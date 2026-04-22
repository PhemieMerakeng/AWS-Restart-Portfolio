## Amazon Aurora: Database Setup and Query Lab

### Project Overview

In this lab, I learned how to work with Amazon Aurora, a cloud-native relational database service offered by AWS. Aurora is fully managed, meaning AWS handles backups, patching, and replication automatically. It is compatible with MySQL and PostgreSQL, but delivers up to five times the performance of standard MySQL.

#### **The goal of this project was to:**
- Create an Aurora database instance from scratch
- Connect to it securely from an EC2 virtual server
- Install the necessary database client tools
- Run SQL commands to create tables, insert data, and query results

This lab gave me hands-on experience with AWS database services that I can apply to real-world cloud applications.

---

#### What is Amazon Aurora?

Amazon Aurora is a database engine built specifically for the cloud. Unlike traditional databases that run on a single server, Aurora uses a distributed storage architecture. Key benefits include:
- High performance: Up to 5x faster than standard MySQL
- High availability: Data is replicated across three Availability Zones
- Automatic scaling: Storage grows automatically up to 128 TB
- Fault tolerant: If one server fails, another takes over without data loss
- Fully managed: AWS handles maintenance, backups, and security patches

#### **Aurora provides two types of endpoints:**
- Writer endpoint: For write operations (INSERT, UPDATE, DELETE)
- Reader endpoint: For read-only queries, with load balancing across replicas

---

### Skills Covered

- **Launching an Amazon Aurora database instance**
- **Configuring VPC and security groups for database access**
- **Connecting to an EC2 instance using AWS Systems Manager Session Manager**
- **Installing MariaDB client on Amazon Linux**
- **Connecting to Aurora using endpoint addresses**
- **Creating tables and running SQL queries**

---

### **Task 1: Create an Aurora Database Instance**

In this task, I created my Aurora database cluster from the AWS Management Console.

#### **Step 1.1: Navigate to RDS Service and Open Databases Dashboard**
- I opened the AWS Management Console. At the top, I searched for RDS and selected the service from the results.
- In the left navigation menu, I clicked Databases
- I clicked the Create database button

#### Step 1.2: Configuring Database 
- **Engine type:** Aurora (MySQL Compatible)
- **Creation method:** Full Configuration (This gave me access to all configuration options)
- **Template:** Dev/Test

<img width="1356" height="520" alt="Screenshot (405)" src="https://github.com/user-attachments/assets/a2e75ec1-3164-466f-8145-6e2cb74bd75b" />

---

<img width="1366" height="156" alt="Screenshot (406)" src="https://github.com/user-attachments/assets/93c17d56-50dc-4cc6-bf29-5cea6cec7e38" />

#### **Step 1.3: Configure Settings**
In the Settings section, I entered:
- **DB cluster identifier:** aurora
- **Master username:** admin
- **Master password:** Admin123Admin321
- **Confirm password:** Admin123Admin321

<img width="1294" height="413" alt="Screenshot (407)" src="https://github.com/user-attachments/assets/c936b395-3dda-48bf-9833-caa572528d04" />

---

<img width="1291" height="429" alt="Screenshot (408)" src="https://github.com/user-attachments/assets/f2ec35e4-b361-4984-943d-24460e6e05cd" />


#### **Step 1.4: Configure Instance Class**
In the Instance configuration section:
- I expanded Burstable classes (includes t classes)
- From the dropdown, I selected db.t3.medium

And for Engine Version:
- **Engine version:** Default option for major version 8.0

<img width="1287" height="425" alt="Screenshot (409)" src="https://github.com/user-attachments/assets/ef37a9de-8728-4a7a-82f0-5070952a95ac" />

#### **Step 1.5: Configure Availability and Durability**
In the Availability & durability section, for Multi-AZ deployment, I selected Don't create an Aurora Replica. For a learning lab, a single instance is sufficient.

<img width="1366" height="158" alt="Screenshot (411)" src="https://github.com/user-attachments/assets/ed71d72a-0022-4937-9dbb-dba6d867ea2f" />

#### **Step 1.6: Configure Connectivity**
In the Connectivity section, I made the following selections:
- **Virtual private cloud (VPC):** LabVPC
- **Subnet group:** dbsubnetgroup
- **Public access:** No
- **VPC security group:** Choose existing and Remove "default", then select "DBSecurityGroup"

<img width="1291" height="483" alt="Screenshot (412)" src="https://github.com/user-attachments/assets/8c1dc8e3-5ae6-4fcb-8242-896a658f83d1" />

---

<img width="1285" height="474" alt="Screenshot (413)" src="https://github.com/user-attachments/assets/3f0c623e-60fe-4e26-932e-4828818cc98d" />

#### **Why these settings matter:**

Public access = No means the database cannot be reached directly from the internet. Only resources inside the VPC can connect.

DBSecurityGroup allows the EC2 instance (Command Host) to connect to the database.

#### **Step 1.7: Complete Remaining Settings and Create Database**
I configured the following settings and launched the database:
- **Monitoring:** Cleared "Enable Enhanced monitoring"
- **Additional** configuration: Entered world as the initial database name
- **Encryption:** Cleared "Enable encryption"
- **Maintenance:** Cleared "Enable auto minor version upgrade"

After reviewing all settings, I scrolled to the bottom and clicked Create database

**Task complete ✓ I successfully created an Aurora database instance.**

---

### **Task 2: Connect to the EC2 Linux Instance**

In this task, I connected to the pre-created EC2 instance named Command Host using AWS Systems Manager Session Manager. This allowed me to run commands directly on the Linux server.

#### **Step 2.1: Navigate to EC2 Service**
- At the top of the AWS Management Console, I searched for EC2 and selected it.
- In the left navigation menu, I clicked Instances.
- I found the instance labelled Command Host, selected the checkbox next to it, and clicked the Connect button at the top.

<img width="1366" height="546" alt="Screenshot (414)" src="https://github.com/user-attachments/assets/b09fadcd-c4e4-42df-9b70-d3b33917d2cc" />

---

<img width="1366" height="351" alt="Screenshot (415)" src="https://github.com/user-attachments/assets/dfc67b87-ce9d-4020-b643-acc6d3f95a69" />

#### **Step 2.2: Connect to the Terminal**
- In the Connect to instance window, I selected the Session Manager tab.
- I clicked the Connect button. A terminal window opened in my browser, giving me command-line access to the EC2 instance.

<img width="1345" height="383" alt="Screenshot (416)" src="https://github.com/user-attachments/assets/ab1adb6e-9219-473a-a727-b7d85236a66e" />

**Task complete ✓ I successfully connected to the EC2 instance**

---

### **Task 3: Configure EC2 to Connect to Aurora**

In this task, I installed the MariaDB client and used it to connect to my Aurora database.

#### **Step 3.1: Install MariaDB Client**
- In the Session Manager terminal, I ran the following command:

<img width="794" height="63" alt="Screenshot (428)" src="https://github.com/user-attachments/assets/aadb9959-f0a9-4afa-bb8b-86c76f0aba9f" />

- The output showed the package downloading and installing. The final line confirmed success

<img width="1348" height="550" alt="Screenshot (417)" src="https://github.com/user-attachments/assets/f2dd0cb2-6011-429b-ae9e-a72d98c0698c" />

#### **Step 3.2: Return to RDS Dashboard**
- I opened a new browser tab, went back to the AWS Management Console, searched for RDS, and clicked Databases in the left menu.
- I clicked on aurora to open the details page.

<img width="1366" height="267" alt="Screenshot (418)" src="https://github.com/user-attachments/assets/a9438587-f685-4edf-9e1e-c73e743dae4e" />

#### **Step 3.3: Copy the Writer Endpoint**
- I selected the Connectivity & security tab. In the Endpoints section, I found the Writer endpoint. I copied the entire endpoint address to a text editor

<img width="1335" height="525" alt="Screenshot (419)" src="https://github.com/user-attachments/assets/7f2d86b9-7e1f-483b-b06b-4f14c3ba3f82" />

#### **Step 3.4: Connect to Aurora**

- Returned to the session manager, used the login and password i created for the aurora database instance to log into aurora
- It required the admin name, password and the endpoint

 e.g  mysql -u admin --password='admin123' -h <endpoint_goes_here>

<img width="1366" height="164" alt="Screenshot (420)" src="https://github.com/user-attachments/assets/3d60fbcd-92e4-4a59-a52a-c5d8ff649604" />

**Task complete ✓ I successfully configured the EC2 instance and connected to the Aurora database.**

### **Task 4: Create a Table and Insert Records**
In this task, I created a database table, inserted country records, and ran queries to retrieve data.

#### **Step 4.1: List Available Databases**
-I ran code to list available Databases 

<img width="948" height="215" alt="Screenshot (421)" src="https://github.com/user-attachments/assets/f93ac34b-4a17-4a7d-8dda-b40fab8f6961" />

#### **Step 4.2: Fixed Error and Switch to the World Database**
- Realized i named my default database 'aurora' instead of 'world' as stated earlier, i deleted it and created a new Database 'world'. After creating it, i ensured it was picked and ready to receive data 

<img width="974" height="377" alt="Screenshot (422)" src="https://github.com/user-attachments/assets/27f117c7-931d-456b-87b5-cb15a9e01ecd" />

#### **Step 4.3: Create the Country Table**
- I created a table to store country information. This table included fields for country code, name, continent, population, GNP, and more.

<img width="1242" height="367" alt="Screenshot (423)" src="https://github.com/user-attachments/assets/2eee0fa9-58a4-48b0-9950-b3242bcc4ab4" />

#### **Step 4.4: Insert Country Records**
- I inserted five records into the country table, one for each country.

<img width="1348" height="358" alt="Screenshot (424)" src="https://github.com/user-attachments/assets/53b05fe3-e5f0-42f5-81f3-bb18ca34bdcf" />

#### **Step 4.5: Query the Table**
I ran a SELECT query to find countries with GNP greater than 35,000 AND population greater than 10 million

<img width="1345" height="270" alt="Screenshot (426)" src="https://github.com/user-attachments/assets/9c1847da-1630-43dc-81de-969057e4bca9" />

**Task complete ✓ I successfully created a table, inserted data, and ran a query returning two results.**

---

### Conclusion
### **I successfully completed all four tasks:**
- **Created an Aurora instance** – I launched a MySQL-compatible Aurora database with custom settings for VPC, security groups, and initial database name.
- **Connected to EC2** – I used Session Manager to access the Command Host Linux instance.
- **Configured EC2 to connect to Aurora** – I installed the MariaDB client and connected using the Aurora writer endpoint.
- **Queried the Aurora instance** – I created a country table, inserted five records, and ran a conditional SELECT query.

This lab gave me practical experience with AWS managed databases. I learned how Aurora differs from standard MySQL, how endpoints work, and how to securely connect cloud resources. These skills are directly applicable to building cloud-native applications.














