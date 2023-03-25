# Week 5 — DynamoDB and Serverless Caching

## Add DynamoDB to docker-compose
```
dynamodb-local:
  #  # https://stackoverflow.com/questions/67533058/persist-local-dynamodb-data-in-volumes-lack-permission-unable-to-open-databa
  #  # We needed to add user:root to get this working.
    user: root
    command: "-jar DynamoDBLocal.jar -sharedDb -dbPath ./data"
    image: "amazon/dynamodb-local:latest"
    container_name: dynamodb-local
    ports:
      - "8000:8000"
    volumes:
      - "./docker/dynamodb:/home/dynamodblocal/data"
    working_dir: /home/dynamodblocal
```

Create bash script (/bin/ddb/schema-load) and run it.
![](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-5/success%20create%20dynamodb.png)

## List Table
Use the documentation here: [dynamodb](https://docs.aws.amazon.com/cli/latest/reference/dynamodb/index.html)
Create bash script (bin/ddb/list-tables)
![](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-5/success%20list%20dynamodb.png)

## Add seed data
Create bash script for export dummy data /bin/ddb/seed
