# Week 0 — Billing and Architecture
## Required Homework

I'm a big fan of terminal and I want to master the skill in this great bootcamp. So, I'll try to use terminal as much as I can to do the homework. <br>
Of course, I'll do the task with the UI first to make me understand the whole new concept. <br>
I found the --cli-auto-prompt is an awesome tool to know the command for make the resources. 
GO GO GO RED SQUAD!!!

### USER CONFIGURATION TASK

Make MFA for Root user
![Activate the MFA for Root](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-0/root-mfa-active.png)

Add new user for cruddur tasks: cruddur-admin, I will use this for daily tasks and not use Root for security.
![Make a new user](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-0/new%20user%20for%20cruddur%20tasks.png)

Add access keys for cruddur-admin: cruddur-daily-tasks
![Access keys for the new user](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-0/access%20keys%20for%20cruddur%20admin.png)

### AWS CLI INSTALLATION TASK
I just follow the instruction for [AWS CLI Installation](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) (I hope it will run smoothly in WSL).<br>

First, I download the zip file for installation. Unzip the file and intall the CLI.
```sh
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

Then, I configure CLI for cruddur-admin use access keys I generated before.
```sh
aws configure list
```
![pow confifure cli](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-0/aws%20configure%20list.png)

### COST & BUDGETING TASK
This is my new AWS account so I make a budgeting alert for Zero-Spend Budget.<br>
And, then I try to make some new budgeting for Cruddur Bootcamp and set the alarm if exceeds $10.
![Make budgeting](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-0/make%20budgets.png)

### AWS ORGANIZATION
In this task, I try the to find my Root OU id, so I can use it for make another OU within. I use this documentation: [AWS Organization CLI Ref](https://docs.aws.amazon.com/cli/latest/reference/organizations/index.html)
```
aws organizations list-roots
```
After, I know the ID then make another OU. They are: Dev OU, Prod OU,  HR OU, and Finance OU. First, I check that my Root OU is empty from another OU. 
```
aws organizations list-organizational-units-for-parent --parent-id ROOT_OU_ID
```
Make Dev and Prod OU under Root OU.
```
aws organizations create-organizational-unit --parent-id ROOT_OU_ID --name Dev\ OU
aws organizations create-organizational-unit --parent-id ROOT_OU_ID --name Prod\ OU
```
Then, make HR OU and Finance OU under Prod OU and use its ID.
```
aws organizations create-organizational-unit --parent-id PROD_OU_ID --name HR\ OU
aws organizations create-organizational-unit --parent-id PROD_OU_ID --name Finance\ OU
```
There you go!
![PoW Make OU with AWS-CLI](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-0/make%20aws%20ou.png)
