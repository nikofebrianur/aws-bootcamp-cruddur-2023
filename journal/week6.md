# Week 6 — Deploying Containers

## Host Static Website in S3 
I use my React note app here: https://github.com/nikofebrianur/notefy-v2.

Run it via Gitpod and build it. Ref: [Deploy React app to S3 & Cloudfront](https://dev.to/karanpratapsingh/deploy-react-app-to-s3-cloudfront-1cao)
```
npm run build
```
Sync the build to S3
```
aws s3 sync build s3://BUCKET-NAME
```
![Success host static web in S3](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-6/url%20link%20static%20web.png)
![Live app](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-6/success%20host%20notefy%20react%20app%20in%20s3.png)
