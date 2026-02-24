# Provisioning an AWS Database Server with Full Application Integration

---

Amazon Relational Database Service (Amazon RDS) makes it easy to set up, operate, and scale a relational database in the cloud. It provides cost-efficient and resizable capacity while managing time-consuming database administration tasks, which allows you to focus on your applications and business. Amazon RDS provides you with six familiar database engines to choose from: Amazon Aurora, Oracle, Microsoft SQL Server, PostgreSQL, MySQL and MariaDB.

---

## Objectives 

- Launch an Amazon RDS DB instance with high availability.

- Configure the DB instance to permit connections from your web server.

- Open a web application and interact with your database

---

#### TASK 1

I created a security group that allows my web server (EC2 instance) to communicate with an Amazon RDS database. The security group acts as a virtual firewall, controlling inbound traffic to the database instance. Specifically, I configured the security group to permit MySQL/Aurora traffic on port 3306 from any instance associated with the Web Security Group. This ensures that only my web server can access the database.

##### Step 1: Access the VPC Dashboard
I logged in to the AWS Management Console. From the Services menu, I selected VPC under the Networking & Content Delivery section.

<img width="1366" height="562" alt="Screenshot (61)" src="https://github.com/user-attachments/assets/ff3a097a-4c34-42ad-bd63-fc2d60df335d" />


---

##### Step 2: Navigate to Security Groups

In the left navigation pane of the VPC Dashboard, I clicked on Security Groups.

<img width="785" height="585" alt="Screenshot (62)" src="https://github.com/user-attachments/assets/27a53322-91ca-47ac-b4ed-31bc5bc3e17c" />

The Security Groups page displayed a list of existing security groups

---

##### Step 3: Create a New Security Group

I clicked the Create security group button.

<img width="1366" height="351" alt="Screenshot (63)" src="https://github.com/user-attachments/assets/4dafc850-ad2e-41cb-ab65-79d5191a6195" />

In the Create security group dialog, I configured the following:
* Security group name: DB Security Group
* Description: Permit access from Web Security Group
* VPC: Selected Lab VPC from the dropdown.
  
<img width="1366" height="443" alt="Screenshot (64)" src="https://github.com/user-attachments/assets/e7f927f3-9961-48b8-85d8-6691a917779c" />

---

##### Step 4: Add an Inbound Rule

<img width="579" height="161" alt="Screenshot (65)" src="https://github.com/user-attachments/assets/73e82f5f-b935-4169-b48b-1e264e979e86" />

In the Inbound rules section, I clicked Add rule.

I configured the rule as follows:
* Type: Selected MySQL/Aurora (this automatically sets the port to 3306).
* Source: I typed sg in the search box to filter security groups, then selected Web Security Group from the list.

<img width="1337" height="228" alt="Screenshot (66)" src="https://github.com/user-attachments/assets/4ed3f1eb-6889-416f-8e05-7d9dfd23f811" />

---

##### Step 5: Review and Create

I scrolled to the bottom of the page and clicked Create security group.

<img width="385" height="59" alt="Screenshot (67)" src="https://github.com/user-attachments/assets/a8c56174-7875-4bce-ae50-4bf4ee2a11f7" />

After a few seconds, a success message appeared confirming the creation of the security group.

<img width="1120" height="390" alt="Screenshot (68)" src="https://github.com/user-attachments/assets/a2ec22d6-d15e-400c-a12b-18733c547b32" />

---
### Task 2

I created a DB Subnet Group, which Amazon RDS uses to determine which subnets and Availability Zones (AZs) can host the database. A DB subnet group must include subnets in at least two AZs to ensure high availability and failover support.ups. Then clicked Create database to launch the instance.

##### Step 1: Open the RDS Console

From the AWS Management Console, I clicked the Services menu and selected RDS under the Database section.

<img width="938" height="528" alt="Screenshot (69)" src="https://github.com/user-attachments/assets/94be0178-3dba-4872-a966-a644669af5c1" />

---

##### Step 2: Navigate to Subnet Groups

In the left navigation pane of the RDS Dashboard, I clicked Subnet groups.

<img width="203" height="136" alt="Screenshot (70)" src="https://github.com/user-attachments/assets/e0cabd06-0d79-40df-b004-0657b5c4b350" />

---

##### Step 3: Start Creating a New Subnet Group

On the Subnet groups page, I clicked the Create DB Subnet Group button.

<img width="1366" height="381" alt="Screenshot (71)" src="https://github.com/user-attachments/assets/4b913af1-5eb2-4588-97be-84adc8fe9144" />

---

##### Step 4: Configure the DB Subnet Group Details

In the Create DB subnet group form, I entered the following:
* Name: DB Subnet Group
* Description: DB Subnet Group
* VPC ID: Selected Lab VPC from the dropdown.

  <img width="1366" height="536" alt="Screenshot (72)" src="https://github.com/user-attachments/assets/9cfb0538-fe53-4384-b612-4c9df8eaaf6b" />

---

##### Step 5: Add Subnets from Two Availability Zones

In the Add subnets section, I needed to select two Availability Zones and their corresponding subnets. First, under Availability zones, I clicked the dropdown and selected the first Availability zone  Then I clicked the dropdown again and selected the second Availability zone 


<img width="1366" height="355" alt="Screenshot (73)" src="https://github.com/user-attachments/assets/0503c647-5892-4cac-9ff6-768cf82ea620" />

After selecting the AZs, the Subnets dropdown(s) appeared. I configured and i selected the private subnets for each Availability Zone

---

##### Step 6: Create the Subnet Group

After verifying the selections, I scrolled down and clicked the Create button. I was redirected back to the Subnet groups list. I located DB Subnet Group and clicked on its name to view details.

<img width="1366" height="251" alt="Screenshot (74)" src="https://github.com/user-attachments/assets/aa181594-ef0f-46e1-8703-77c50cf2535d" />

---

### Task 3 

I created a Multi-AZ Amazon RDS for MySQL database instance. Multi-AZ deployments enhance availability and durability by automatically provisioning and synchronously replicating data to a standby instance in a different Availability Zone. This configuration is ideal for production workloads, but for this lab, I used the Dev/Test template to keep costs low while still demonstrating the setup.

##### Step 1: Navigate to RDS and Start Database Creation

In the AWS Management Console, I opened the Services menu and selected RDS under Database.
In the left navigation pane, I clicked Databases. I clicked the Create database button

<img width="1366" height="407" alt="Screenshot (75)" src="https://github.com/user-attachments/assets/1c920d00-34be-45c7-aad5-cb37a7fb639f" />

---

##### Step 2: Choose Database Creation Method and Engine On the Create database page, I ensured Full Configuration create was selected

<img width="1366" height="316" alt="Screenshot (76)" src="https://github.com/user-attachments/assets/1b7c6c78-b621-4846-9498-ad3d6626bb4c" />

Under Engine options:
* Engine type: I selected MySQL.

  <img width="1366" height="350" alt="Screenshot (77)" src="https://github.com/user-attachments/assets/011253ab-a49d-476a-938e-eedec8d33f71" />

---

##### Step 3: Choose Template and Availability & Durability
Under Templates, I selected Dev/Test (to use free tier eligible settings where possible).

<img width="1366" height="357" alt="Screenshot (78)" src="https://github.com/user-attachments/assets/989892e6-c189-4164-80db-081283a64d0b" />

Under Availability and durability, I selected Multi-AZ DB Instance.
This option tells RDS to create a primary and a standby instance in different AZs for high availability

<img width="1366" height="469" alt="Screenshot (79)" src="https://github.com/user-attachments/assets/0b9ef267-8e5a-4026-9f4f-5ff3c4f80b2c" />

---

##### Step 4: Configure Settings (Database Credentials)
In the Settings section, I set:
* DB instance identifier: lab-db
* Master username: main
  
<img width="1366" height="334" alt="Screenshot (80)" src="https://github.com/user-attachments/assets/5ee04ddd-5bdd-405d-b5d0-86069cd83038" />

* Master password: lab-password
* Confirm password: lab-password

  <img width="1366" height="501" alt="Screenshot (81)" src="https://github.com/user-attachments/assets/44f7af0e-5b5c-4cac-99b6-8f85d8f51f81" />

 ---
 
##### Step 5: Choose DB Instance Class

Under Instance configuration:
* I clicked the Burstable classes (includes t classes) filter to see T-series instances.
* I selected db.t3.medium from the list.

<img width="1366" height="433" alt="Screenshot (82)" src="https://github.com/user-attachments/assets/3a87b066-9bef-49d6-8335-0904f5675d91" />

---

##### Step 6: Configure Storage

Under Storage:
* Storage type: I selected General Purpose (SSD).
  (I left other storage settings at defaults.)
  
<img width="1366" height="450" alt="Screenshot (83)" src="https://github.com/user-attachments/assets/0afec20f-0d97-4064-a581-d6a40faf744f" />

##### Step 7: Configure Connectivity

Under Connectivity:

* Virtual Private Cloud (VPC): I selected Lab VPC.
* VPC security group: I chose Choose existing.
* Under Existing VPC security groups, I:
* Used the X to remove the default security group.
* Selected DB Security Group

<img width="1366" height="577" alt="Screenshot (84)" src="https://github.com/user-attachments/assets/f950b07b-d27f-4e5b-9d45-cc28a023f72b" />


<img width="1366" height="575" alt="Screenshot (85)" src="https://github.com/user-attachments/assets/13dc0562-63b6-4f78-b8ee-ccde428505bb" />


#### The DB Security Group was created in Task 1 and allows inbound MySQL traffic from the Web Security Group. This ensures our web server can connect to the database.

---

##### Step 8: Adjust Monitoring and Additional Configuration

Under Monitoring, I expanded the Additional configuration .
Enhanced Monitoring: I unchecked Enable Enhanced monitoring to simplify the lab (this reduces cost and speeds up creation)

<img width="1366" height="567" alt="Screenshot (86)" src="https://github.com/user-attachments/assets/555a00d3-867d-4f10-89bc-371e4dc09400" />

---

##### Step 9: Configure Database Options (Initial Database Name)
I scrolled down to the Additional configuration section (separate from Monitoring) and expanded it.

Under Database options:
* Initial database name: I entered lab.

Under Backup:
* I unchecked Enable automated backups.
   This is not recommended for production, but for the lab it makes the database deploy faster.


<img width="1366" height="575" alt="Screenshot (87)" src="https://github.com/user-attachments/assets/9e68f646-1db3-4aeb-89b4-3a62f022d36b" />

---

##### Step 10: Create the Database

After reviewing all settings, I scrolled to the bottom of the page and clicked Create database.
Screenshot: Create database button at the bottom. The database instance status showed Creating. It took a few minutes for the instance to be provisioned.

<img width="1366" height="311" alt="Screenshot (88)" src="https://github.com/user-attachments/assets/f4926d1b-baaf-4a51-82e9-c598403b346b" />

---

### Task 4 

##### Step 1: Retrieve the RDS Endpoint

In the AWS Management Console, I navigated to RDS → Databases.
I clicked on the DB identifier lab-db.
Under the Connectivity & security tab, I located the Endpoint

<img width="1366" height="569" alt="Screenshot (92)" src="https://github.com/user-attachments/assets/fb6c5d8a-1632-4381-ae77-7bd05907b8b4" />


---

##### Step 2: Connect to the EC2 Instance using PuTTY

---

##### Step 3: Switch to Root User

Once logged in, I elevated privileges by running:
##### sudo su

<img width="1345" height="685" alt="Screenshot (89)" src="https://github.com/user-attachments/assets/1bc0a986-bc64-458c-b471-9e939c138904" />


---

##### Step 4: Connect to the RDS Database
With the MySQL client ready, I used the following command to connect to the database:

mysql -h lab-db.xxxxxxxxxx.us-east-1.rds.amazonaws.com -u main -p lab

<img width="1329" height="691" alt="Screenshot (95)" src="https://github.com/user-attachments/assets/86f528e2-3085-4d67-a247-d544d2ef6800" />








  










