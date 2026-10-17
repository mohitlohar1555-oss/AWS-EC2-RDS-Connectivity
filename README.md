
# AWS EC2 and RDS Connectivity Project

## Project Overview

This project demonstrates how to connect an Amazon EC2 Ubuntu instance to an Amazon RDS MySQL database securely using AWS Console configuration and security groups.

The project covers database creation, EC2 instance deployment, network connectivity, MySQL client installation, and database connection testing.

## Project Objectives

- Create an Amazon RDS MySQL database.
- Launch an Ubuntu EC2 instance.
- Configure secure connectivity between EC2 and RDS.
- Install the MySQL client on EC2.
- Connect to RDS using its endpoint.
- Test database connectivity using SQL commands.

## AWS Services Used

- **Amazon EC2** – Virtual server running Ubuntu.
- **Amazon RDS** – Managed MySQL relational database.
- **VPC** – Provides network isolation and connectivity.
- **Security Groups** – Control traffic between EC2 and RDS.
- **AWS Management Console** – Configure and manage AWS resources.

## Architecture

```text
          Administrator
                |
                v
        AWS Management Console
                |
        +-------+-------+
        |               |
        v               v
   Amazon EC2       Amazon RDS
   Ubuntu Server    MySQL Database
        |               |
        | MySQL Client  |
        +------->-------+
          TCP Port 3306
        Private Connectivity
```

## Project Configuration

| Component | Configuration |
|---|---|
| AWS Region | Asia Pacific (Sydney) |
| Region Code | ap-southeast-2 |
| EC2 Operating System | Ubuntu |
| EC2 Instance Type | t3.micro |
| EC2 Instance Name | EC2-RDS |
| Database Engine | MySQL |
| RDS Identifier | database-1 |
| Master Username | admin |
| Database Port | 3306 |
| MySQL Client | mysql-client |

*Note: These settings reflect the configuration documented in the project PDF. Availability and pricing depend on your AWS account and current AWS offerings.*

## Implementation Steps

### Step 1: Create an Amazon RDS Database

1. Open the AWS Management Console.
2. Navigate to Amazon RDS.
3. Select **Create database**.
4. Choose **Full configuration**.
5. Select MySQL as the database engine.
6. Choose an appropriate template.
7. Configure the DB identifier and master username.
8. Set a strong database password.
9. Configure storage and create the database.
10. Wait until the database status becomes `Available`.

### Step 2: Launch an EC2 Instance

1. Open the Amazon EC2 console.
2. Click **Launch instance**.
3. Enter the instance name `EC2-RDS`.
4. Select Ubuntu as the operating system.
5. Choose an appropriate instance type.
6. Configure the key pair and network settings.
7. Review the configuration and launch the instance.
8. Wait for the instance to reach the `Running` state.
9. Connect to the instance terminal.

Update the Ubuntu package list:

```bash
sudo apt update -y
```

### Step 3: Configure EC2-to-RDS Connectivity

1. Open the RDS database details.
2. Confirm that the database status is `Available`.
3. Find **Connected compute resources**.
4. Select **Set up EC2 connection**.
5. Choose the EC2 instance.
6. Review the security group changes.
7. Complete the setup.

The connection setup in this project configures security groups to allow the EC2 instance to communicate with RDS on TCP port `3306`.

### Step 4: Install the MySQL Client

Run the following command on the Ubuntu EC2 instance:

```bash
sudo apt-get install mysql-client -y
```

### Step 5: Find the RDS Endpoint

1. Open the RDS database.
2. Select **Connectivity & security**.
3. Find the database endpoint.
4. Copy the endpoint hostname.
5. Confirm the MySQL port is `3306`.

### Step 6: Connect EC2 to RDS

Run the following command from the EC2 terminal:

```bash
mysql -u admin -h <RDS-ENDPOINT> -P 3306 -p
```

Replace `<RDS-ENDPOINT>` with your actual RDS endpoint.

Enter the database master password when prompted.

**Important:** Do not include angle brackets around the endpoint in the actual command.

### Step 7: Test the Database Connection

After connecting successfully, execute:

```sql
SHOW DATABASES;
```

The default MySQL databases should appear, including:

- information_schema
- mysql
- performance_schema
- sys

You can also create a test database:

```sql
CREATE DATABASE testdb;
```

Verify it exists:

```sql
SHOW DATABASES;
```

## Security Best Practices

- Keep the RDS database private unless public access is explicitly required.
- Allow inbound MySQL traffic on port `3306` only from the EC2 security group.
- Never expose the MySQL port to `0.0.0.0/0`.
- Restrict SSH access to your own IP address.
- Use a strong, unique database password.
- Consider AWS Secrets Manager for credential management.
- Never commit passwords, private keys, or AWS credentials to GitHub.
- Remove unused AWS resources to avoid unnecessary charges.

## Troubleshooting

| Problem | Solution |
|---|---|
| Connection timed out | Check security groups, VPC, routing, and network access. |
| Access denied for user | Verify the username and password. |
| Unknown MySQL host | Check the RDS endpoint spelling. |
| Cannot connect to local MySQL socket | Use `-h <RDS-ENDPOINT>` to connect to RDS instead of a local MySQL server. |
| Database not available | Wait until the RDS status becomes `Available`. |

## Learning Outcomes

By completing this project, I practiced:

- Deploying an EC2 Ubuntu instance.
- Creating a managed MySQL database using Amazon RDS.
- Configuring security groups for database connectivity.
- Connecting to a remote database using a MySQL client.
- Running SQL commands to verify connectivity.
- Applying basic AWS networking and security practices.

## Project Documentation

This repository includes a step-by-step PDF guide with AWS Console screenshots.

**Documentation:** `RDS with EC2 connection.pdf`

## Author

**Mohit Gadilohar**

Aspiring Cloud Engineer | DevOps with AWS

- LinkedIn: (www.linkedin.com/in/mohit-gadilohar-devops)
- GitHub: (https://github.com/mohitlohar1555-oss)

---

If you found this project useful, feel free to explore the repository and connect with me on LinkedIn.
