# Provisioning an AWS Database Server with Full Application Integration

---

Amazon Relational Database Service (Amazon RDS) makes it easy to set up, operate, and scale a relational database in the cloud. It provides cost-efficient and resizable capacity while managing time-consuming database administration tasks, which allows you to focus on your applications and business. Amazon RDS provides you with six familiar database engines to choose from: Amazon Aurora, Oracle, Microsoft SQL Server, PostgreSQL, MySQL and MariaDB.

---

## Objectives 

- Launch an Amazon RDS DB instance with high availability.

- Configure the DB instance to permit connections from your web server.

- Open a web application and interact with your database

---

### Phase 1: Provisioning the MySQL Database

#### Initializing the Database

I navigated to the RDS Console, clicked Databases, and selected Create database. I chose the Standard create flow and selected MySQL as the Engine type with the latest version.

---

#### Template and High Availability

I selected the Dev/Test template, then scrolled to the Availability and durability section and selected the Multi-AZ DB Instance.

---

#### Settings and Credentials

Under Settings, I set the DB instance identifier to lab-db and configured the master username as main set my password

---

#### Instance and Storage

Under Instance configuration, I selected Burstable classes and chose the db.t3.medium size. For storage, I kept the default General Purpose (SSD)

---

#### Connectivity and Security

I selected the Lab VPC and switched the security group setting to Choose existing. I removed the default group and selected the DB Security Group

---

#### Additional Configurations and Launch

I expanded Additional configuration to uncheck Enable Enhanced monitoring. Under the second Additional configuration section, I set the initial database name to lab and unchecked Enable automated backups. Finally, I clicked Create database to launch the instance.

---

#### Retrieving the Database Endpoint

I clicked the lab-db link to view the instance details. I then scrolled down to the Connectivity & security section and copied the Endpoint field to use for the application connection.

---

### Phase 2: Connecting the Web Application to the RDS Instance

#### Accessing the Web Server

I retrieved the WebServer IP address from the AWS details and pasted it into a new browser tab. Once the application loaded, I clicked the RDS link at the top of the page to begin the database configuration.

---

#### Configuring the Database Connection

In the configuration form, I entered the following credentials to link the app to the DB server:

Endpoint: [Pasted the RDS Endpoint]

Database: lab

Username: main

Password: lab-password

I then clicked Submit and waited for the application to initialize the database schema

---

#### Testing Data Persistence and Replication

Once the Address Book appeared, I tested the full-stack integration by adding, editing, and removing contacts. Because the database was configured for Multi-AZ, this data was automatically replicated to a standby instance in a second Availability Zone for high availability.

