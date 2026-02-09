#EC2 Hands-on Instance Setup Lab

Amazon Elastic Compute Cloud (EC2) provides scalable, on-demand computing power through a streamlined web interface. It allows developers to maintain full control over their virtual resources within Amazon’s reliable environment while removing the friction of managing physical hardware.

​The primary advantage of EC2 is its incredible agility; new server instances can be provisioned and booted in just minutes. This enables dynamic scaling, allowing you to instantly expand or contract capacity to match shifting technical requirements or traffic spikes, ensuring both performance and cost-efficiency.

​Through this lab, I gained a practical overview of the EC2 lifecycle, including launching, resizing, and monitoring instances.

---
##Key Concepts Covered 
*Launching a web server with termination protection enabled
*Monitoring EC2 Instances 
*Modifying security groups for HTTP access
*Resizing instances to scale 
*Terminating EC2 instances

---

###I accessed the AWS Web Console and on the search bar typed EC2 and selected the EC2 option. On the dashboard pane, I scrolled to the bottom and selected Launch Instance.

###Naming the Instance

I started by naming the instance Web Server in the Name and tags pane, which automatically assigned the "Name" key-value pair to the resource.

---

###Choosing an AMI

In the Application and OS Images section, I kept the default Amazon Linux 2023 AMI to serve as the template for my instance's root volume and OS.

---

###Selecting Instance Type

I selected t3.micro from the instance type dropdown, providing a balance of 2 vCPUs and 1 GiB of memory for the workload.

---

###Configuring Key Pair

Since I didn't need to log in to the instance for this specific task, I selected Proceed without a key pair in the login pane.

---

###Network Settings

I edited the Network settings to launch the instance into the Lab VPC. I then created a new security group named Web Server security group and removed the default SSH inbound rule to harden security.

---

###Adding Storage

I opted to use the default 8 GiB Amazon EBS root volume provided in the Configure storage pane.

---

###Advanced Details

In the Advanced details section, I enabled Termination protection to prevent accidental deletion and prepared the User data field to run automated configuration scripts upon startup.

---

###Configuring Advanced Details

I expanded the Advanced details pane and enabled Termination protection to prevent accidental deletion. To automate the setup, I added a script to the User data field that installs the Apache web server, configures it to start on boot, and creates a custom "Hello" HTML landing page.

---

###Launching the Instance

I clicked Launch instance and navigated to View all instances. I waited for the Instance State to turn to "Running" and for Status Checks to show "2/2 checks passed," confirming the instance was successfull and the hardware and software were properly launched.

---

###Monitoring the Instance

I explored the Status checks and Monitoring tabs to view CloudWatch metrics and reachability data. I also used the Get Instance Screenshot tool under the "Monitor and troubleshoot" menu to visually verify the instance's console status.

---

###Updating Security Groups

I located my Public IPv4 address in the Details tab of my selected instance and copied it to my browser. Initially, the page failed to load because the current security group acted as a firewall blocking all inbound traffic. To resolve this I navigated to Security Groups and selected Edit inbound rules. I used the Type dropdown to select HTTP and the Source dropdown to select Anywhere-IPv4.

---

###Launching the Instance

I finalized the configuration by clicking Launch instance in the summary pane on the right. After selecting View all instances, I monitored the status in the main Instances console. I waited until the Instance state column showed Running and the Status checks column displayed 2/2 checks passed, confirming the OS and hardware were ready.

---

###Monitoring the Instance

To verify the health of the server, I checked the box next to my instance and looked at the tabs in the bottom pane. I first reviewed the Status checks tab to confirm system and instance reachability. I then switched to the Monitoring tab to view CloudWatch metrics like CPU utilization. Finally, I went to the Actions menu, navigated to Monitor and troubleshoot, and selected Get instance screenshot to see a visual capture of the instance’s console boot sequence.

---

###Updating Security Groups

I located my Public IPv4 address in the Details tab (bottom pane) and pasted it into a new browser tab. The page wouldn't load because port 80 was blocked. To fix this, I went to the left navigation pane, selected Security Groups under Network & Security, and chose my Web Server security group. In the Inbound rules tab, I clicked Edit inbound rules, added a rule where the Type dropdown was set to HTTP and the Source dropdown was set to Anywhere-IPv4. After saving, I refreshed my browser to see the "Hello From Your Web Server!" message.

---

###Resizing the Instance and Volume

To scale the server, I first went to the Instance state menu and selected Stop instance. Once the state showed Stopped, I used the Actions menu to go to Instance settings then sellected Change instance type and updated it to t3.small. Next, I went to the left sidebar, selected Volumes under Elastic Block Store where I checked my volume, and clicked Actions then Modify Volume to increase the size from 8 GiB to 10 GiB. I then returned to the Instances page and restarted the server.

---

###Testing Termination Protection

I attempted to delete the server by selecting Instance state then Terminate instance, but the operation failed due to the protection I enabled during setup. To delete it, I had to go to the Actions menu, select Instance settings then Change termination protection, and uncheck the Enable box. Once I saved that change, I was able to use the Terminate option to permanently delete the instance.
