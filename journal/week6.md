# Week 6 — Deploying Containers

## Host Static Website in S3 
I use my React note app here: https://github.com/nikofebrianur/notefy-v2.

Run it via Gitpod and build it. Ref: [Deploy React app to S3 & Cloudfront](https://dev.to/karanpratapsingh/deploy-react-app-to-s3-cloudfront-1cao)
```sh
npm run build
```
Sync the build to S3
```sh
aws s3 sync build s3://BUCKET-NAME
```
![Success host static web in S3](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-6/url%20link%20static%20web.png)

Here the live React app shows:
![Live app](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-6/success%20host%20notefy%20react%20app%20in%20s3.png)

## Create CloudFront Distribution
Ref: [CloudFront AWS CLI Docs](https://docs.aws.amazon.com/cli/latest/reference/cloudfront/create-distribution.html)

This time, I use console to make the distribution in CloudFront.
At first time, I use the website endpoint so the OAI doesn't show and all clear with this ref: [CloudFront OAI](https://www.stormit.cloud/blog/cloudfront-origin-access-identity/)
[](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-6/use%20cloudfront.png).

And it is live with CloudFront URL:
![Live CloudFront](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-6/cloudfront%20url.png)

Following the ECS video and reach to this point. I created the service for notefy frontend:
![](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-6/svc%20notefy.png)
