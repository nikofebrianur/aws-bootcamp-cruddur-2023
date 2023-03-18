# Week 4 — Postgres and RDS
## Configure docker-compose.yml
Add this:
```
db:
    image: postgres:13-alpine
    restart: always
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=password
    ports:
      - '5432:5432'
    volumes: 
      - db:/var/lib/postgresql/data
```
![success deploy](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-4/all%20success%20docker.png)

## Postgres DB Configuration
Connect to psql via the psql client cli tool
```
psql -Upostgres --host localhost
```

Create the database
```
CREATE database cruddur;
```

### Import Script
Create a new SQL file called schema.sql and place it in backend-flask/db

The command to import:
```
psql cruddur < db/schema.sql -h localhost -U postgres
```

### Add UUID Extension
We are going to have Postgres generate out UUIDs. We'll need to use an extension called:
```
CREATE EXTENSION "uuid-ossp";
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";
```

Run the script
```
psql -U postgres cruddur < backend-flask/db/schema.sql -h localhost
```

## Create RDS Postgres with AWS CLI
```
aws rds create-db-instance \
  --db-instance-identifier cruddur-db-instance \
  --db-instance-class db.t3.micro \
  --engine postgres \
  --engine-version  14.6 \
  --master-username cruddurroot \
  --master-user-password xxxxxx \
  --allocated-storage 20 \
  --availability-zone ca-central-1a \
  --backup-retention-period 0 \
  --port 5432 \
  --no-multi-az \
  --db-name cruddur \
  --storage-type gp2 \
  --publicly-accessible \
  --storage-encrypted \
  --enable-performance-insights \
  --performance-insights-retention-period 7 \
  --no-deletion-protection
```
![success create rds](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-4/success%20deploy%20rds%20with%20cli.png)

## Connect to RDS Prod with Gitpod
Get Gitpod IP
```
GITPOD_IP=$(curl ifconfig.me)
```

And then, paste the ip to inbound rule (security group) or use AWS CLI below:
```
aws ec2 modify-security-group-rules \
    --group-id $DB_SG_ID \
    --security-group-rules "SecurityGroupRuleId=$DB_SG_RULE_ID,SecurityGroupRule={Description=GITPOD,IpProtocol=tcp,FromPort=5432,ToPort=5432,CidrIpv4=$GITPOD_IP/32}"
```

Let's connect it.
```
psql $PROD_CONNECTION_URL
```
![success deploy in prod](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-4/success%20connect%20to%20prod%20pg.png)
