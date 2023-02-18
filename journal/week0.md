# Week 0 — Billing and Architecture
## Required Homework

### USER CONFIGURATION TASKS

Make MFA for Root user
![Activate the MFA for Root](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-0/root-mfa-active.png)

Add new user for cruddur tasks: cruddur-admin, I will use this for daily tasks and not use Root for security.
![Make a new user](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-0/new%20user%20for%20cruddur%20tasks.png)

Add access keys for cruddur-admin: cruddur-daily-tasks
![Access keys for the new user](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-0/access%20keys%20for%20cruddur%20admin.png)

### Install AWS CLI via WSL2.
I just follow the instruction for [AWS CLI Installation](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) (I hope it will run smoothly in WSL).
First, I download the zip file for installation.


Then, I configure CLI for cruddur-admin use access keys I generated before.
![pow confifure cli](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-0/aws%20configure%20list.png)

### COST & BUDGETING TASKS
This is my new AWS account so I make a budgeting alert for Zero-Spend Budget.
And, then I try to make some new budgeting for Cruddur Bootcamp and set the alarm if exceeds $10.
![Make budgeting](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-0/make%20budgets.png)
