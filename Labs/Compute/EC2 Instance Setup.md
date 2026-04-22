# EC2 Hands-on Instance Setup Lab

Amazon Elastic Compute Cloud (EC2) provides scalable, on-demand computing power through a streamlined web interface. It allows developers to maintain full control over their virtual resources within Amazon’s reliable environment while removing the friction of managing physical hardware.

​The primary advantage of EC2 is its incredible agility; new server instances can be provisioned and booted in just minutes. This enables dynamic scaling, allowing you to instantly expand or contract capacity to match shifting technical requirements or traffic spikes, ensuring both performance and cost-efficiency.

​Through this lab, I gained a practical overview of the EC2 lifecycle, including launching, resizing, and monitoring instances.

---
## Key Concepts Covered 
* Launching a web server with termination protection enabled
* Monitoring EC2 Instances 
* Modifying security groups for HTTP access
* Resizing instances to scale 
* Terminating EC2 instances

---

### Accessing AWS

I accessed the AWS Web Console and on the search bar typed EC2 and selected the EC2 option. On the dashboard pane, I scrolled to the bottom and selected Launch Instance.

<img width="1049" height="571" alt="Screenshot (4)" src="https://github.com/user-attachments/assets/5c6e2267-9b79-4a9e-a023-95f529c6245d" />

--

<img width="1366" height="581" alt="168402" src="https://github.com/user-attachments/assets/a4ea0485-cc26-4a8e-8307-8113cdfe862a" />

--

<img width="630" height="574" alt="168403" src="https://github.com/user-attachments/assets/6eab5625-ed7c-46e6-bc45-46c585737759" />

---

### Naming the Instance

I started by naming the instance Web Server in the Name and tags pane

<img width="912" height="343" alt="Screenshot (8)" src="https://github.com/user-attachments/assets/86d83e97-04d0-42b6-88d2-c7a01fdbb7cf" />

---

### Choosing an AMI

In the Application and OS Images section, I kept the default Amazon Linux 2023 AMI to serve as the template for my instance's root volume and OS.

![Screenshot_20260208_230710_Gmail](https://github.com/user-attachments/assets/03ee1a8a-cf0e-4488-9199-4b9cc3e0a0ac)

---

### Selecting Instance Type

I selected t3.micro from the instance type dropdown, providing a balance of 2 vCPUs and 1 GiB of memory for the workload.

<img width="890" height="276" alt="168408" src="https://github.com/user-attachments/assets/bfa70da5-7ca9-4dcf-a1cd-1375fa8be347" />

---

### Configuring Key Pair

Since I didn't need to log in to the instance for this specific task, I selected Proceed without a key pair in the login pane.

<img width="870" height="218" alt="168409" src="https://github.com/user-attachments/assets/e39951f4-0e8f-49a4-881d-2433e3cfb696" />

---

### Network Settings

I edited the Network settings to launch the instance into the Lab VPC. I then created a new security group named Web Server security group and removed the default SSH inbound rule to harden security.

<img width="877" height="475" alt="168410" src="https://github.com/user-attachments/assets/4f070876-b82f-475f-bc6c-26ab82b5c2aa" />

I opted to use the default 8 GiB Amazon EBS root volume provided in the Configure storage pane.

---

### Advanced Details

I expanded the Advanced details pane and enabled Termination protection to prevent accidental deletion. To automate the setup, I added a script to the User data field that installs the Apache web server, configures it to start on boot, and creates a custom "Hello" HTML landing page.

<img width="893" height="570" alt="168411" src="https://github.com/user-attachments/assets/9daf03c7-6302-4216-b723-a739c94206f3" />

--

<img width="566" height="425" alt="168412" src="https://github.com/user-attachments/assets/7d71962c-2b56-483e-98a5-302cbfad4e9f" />

---

### Launching the Instance

I clicked Launch instance and navigated to View all instances. I waited for the Instance State to turn to "Running" and for Status Checks to show "2/2 checks passed," confirming the instance was successfull and the hardware and software were properly launched.

<img width="1366" height="201" alt="Screenshot (15)" src="https://github.com/user-attachments/assets/cf03b0d4-352c-4add-b058-6c0f6f3cc568" />

--

<img width="1123" height="246" alt="Screenshot (16)" src="https://github.com/user-attachments/assets/a1e34a62-324c-417c-bbad-5b1174f8832e" />

---

### Monitoring the Instance

I explored the Status checks and Monitoring tabs to view CloudWatch metrics and reachability data. I also used the Get Instance Screenshot tool under the "Monitor and troubleshoot" menu to visually verify the instance's console status.

![i-03fe70e4a6f7afe5a](https://github.com/user-attachments/assets/e84af3e5-c802-4587-9cab-7f4f60c1849e)

---

### Updating Security Groups

I located my Public IPv4 address in the Details tab (bottom pane) and pasted it into a new browser tab. The page wouldn't load because port 80 was blocked. To fix this, I went to the left navigation pane, selected Security Groups under Network & Security, and chose my Web Server security group. In the Inbound rules tab, I clicked Edit inbound rules, added a rule where the Type dropdown was set to HTTP and the Source dropdown was set to Anywhere-IPv4. After saving, I refreshed my browser to see the "Hello From Your Web Server!" message.

<img width="1366" height="680" alt="Screenshot (17)" src="https://github.com/user-attachments/assets/6ea35a57-c493-4243-95c7-f1e0336a97df" />

--

<img width="1366" height="665" alt="Screenshot (18)" src="https://github.com/user-attachments/assets/8cd9d0b1-d1a2-488b-940e-b56083369db6" />

---

### Resizing the Instance and Volume

To scale the server, I first went to the Instance state menu and selected Stop instance. 

<img width="1098" height="247" alt="Screenshot (19)" src="https://github.com/user-attachments/assets/211d036c-9bc4-47e4-95c9-bfc24f77b224" />

Once the state showed Stopped, I used the Actions menu to go to Instance settings then sellected Change instance type.

<img width="675" height="417" alt="Screenshot (21)" src="https://github.com/user-attachments/assets/e1d8dfd5-4d67-444d-9ff5-347ebd11daac" />

I then updated it to t3.small. Next, I went to the left sidebar, selected Volumes under Elastic Block Store where I checked my volume, and clicked Actions then Modify Volume to increase the size from 8 GiB to 10 GiB. I then returned to the Instances page and restarted the server.

<img width="855" height="423" alt="Screenshot (22)" src="https://github.com/user-attachments/assets/b1d408c4-afb5-48a3-9817-364ec05f9894" />

--

<img width="449" height="572" alt="540723624-e1d784c9-63fb-4d62-882b-cfc5f3cea335" src="https://github.com/user-attachments/assets/8db7ff73-9a46-4ffc-9c7a-be744037cdf5" />

--

<img width="1124" height="463" alt="Screenshot (24) (1)" src="https://github.com/user-attachments/assets/61f4b1bf-b11a-44c3-85b2-6d11dd05d304" />

---

### Testing Termination Protection

I attempted to delete the server by selecting Instance state then Terminate instance, but the operation failed due to the protection I enabled during setup. 

<img width="940" height="507" alt="540727653-c644ce28-b80c-4ed7-ac61-ab9801b4c312" src="https://github.com/user-attachments/assets/d0a1f96e-d3bf-45ff-a79c-89d26857c716" />

--

<img width="521" height="356" alt="540728653-86ac8b81-65ee-41b3-a67b-dd2115d69146" src="https://github.com/user-attachments/assets/a1493347-0cd0-459e-b2a2-9f7a9ce5a383" />

To delete it, I had to go to the Actions menu, select Instance settings then Change termination protection, and uncheck the Enable box.

<img width="637" height="416" alt="540498735-546b97ea-b357-42aa-b3e0-abfd92457c6f" src="https://github.com/user-attachments/assets/4422e7f1-8c3e-42fa-bf8a-1c831acc1653" />

Once I saved that change, I was able to use the Terminate option to permanently delete the instance.

<img width="474" height="229" alt="540499065-e259e8d9-097b-44ea-b831-37dc7f022f62" src="https://github.com/user-attachments/assets/ad73e6e8-fea5-4e00-a453-3ab9caa94a4b" />

--

<img width="747" height="434" alt="540499085-5c3361b3-80b4-4715-a6d1-b7b3ad2ab04b" src="https://github.com/user-attachments/assets/8da12179-799c-4087-b5fb-5dcbcb37a052" />




