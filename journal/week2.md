# Week 2 — Distributed Tracing

## Instrument HoneyComb and OpenTelemetry
Following the steps in live video here and success to get logs
![](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-2/success%20honeycomb-flask%20integration.png)
![](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-2/flask%20span%20query.png)

## Configure AWS X-Ray
Add environment in docker compose file:
```sh
AWS_XRAY_URL: "*4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}*"
AWS_XRAY_DAEMON_ADDRESS: "xray-daemon:2000"
```

Create group for X-Ray trace:
```sh
aws xray create-group --group-name "Cruddur" --filter-expression "service(\"backend-flask\")"
```
![](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-2/x%20ray%20trace%20group.png)

Create X-Ray sampling rule:
```sh
aws xray create-sampling-rule --cli-input-json file://aws/json/xray.json
```
![](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-2/x%20ray%20sampling%20rule.png)

Create AWS X-Ray daemon service to Docker Compose:
```sh
xray-daemon:
    image: "amazon/aws-xray-daemon"
    environment:
      AWS_ACCESS_KEY_ID: "${AWS_ACCESS_KEY_ID}"
      AWS_SECRET_ACCESS_KEY: "${AWS_SECRET_ACCESS_KEY}"
      AWS_REGION: "ca-central-1"
    command:
      - "xray -o -b xray-daemon:2000"
    ports:
      - 2000:2000/udp
```

Export this code to app.py:
```
from aws_xray_sdk.core import xray_recorder
from aws_xray_sdk.ext.flask.middleware import XRayMiddleware
```
Use dynamic naming for X-Ray URL:
```
xray_url = os.getenv("AWS_XRAY_URL")
xray_recorder.configure(service='backend-flask', dynamic_naming=xray_url)
```
After the configuration done, you can run
```sh
docker compose -f "docker.compose.yml" up -d --build
