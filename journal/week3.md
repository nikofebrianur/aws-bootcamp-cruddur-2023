# Week 3 — Decentralized Authentication

## Homework Task
### Implement JWT Middleware in Flask App
For this task, I found an [article](https://www.loginradius.com/blog/engineering/guest-post/securing-flask-api-with-jwt/) and try to follow the steps.

Add new library for the requirement.
```
pyjwt 
pillow
```
And, make new file for the middleware and then implement it in app.py

I implement the JWT in /api/activities/home endpoint and I think it works because it shows error page :D
![error page yeay](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-3/jwt%20in%20home%20endpoint.png)

## Live Streaming 
### Implement Amplify and Cognito
```
npm i aws-amplify
```
import { Amplify } from 'aws-amplify';

Amplify.configure({
  "AWS_PROJECT_REGION": process.env.REACT_APP_AWS_PROJECT_REGION,
  "aws_cognito_region": process.env.REACT_APP_AWS_COGNITO_REGION,
  "aws_user_pools_id": process.env.REACT_APP_AWS_USER_POOLS_ID,
  "aws_user_pools_web_client_id": process.env.REACT_APP_CLIENT_ID,
  "oauth": {},
  Auth: {
    // We are not using an Identity Pool
    // identityPoolId: process.env.REACT_APP_IDENTITY_POOL_ID, // REQUIRED - Amazon Cognito Identity Pool ID
    region: process.env.REACT_APP_AWS_PROJECT_REGION,           // REQUIRED - Amazon Cognito Region
    userPoolId: process.env.REACT_APP_AWS_USER_POOLS_ID,         // OPTIONAL - Amazon Cognito User Pool ID
    userPoolWebClientId: process.env.REACT_APP_CLIENT_ID,   // OPTIONAL - Amazon Cognito Web Client ID (26-char alphanumeric string)
  }
});
