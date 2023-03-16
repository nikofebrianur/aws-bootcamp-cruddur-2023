# Week 4 — Postgres and RDS

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
