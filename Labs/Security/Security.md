## AWS Identity and Access Management (IAM)

### Overview
In many business environments, a single login can grant access to all network resources—from shared folders to printers and servers. While convenient, this approach can become a security nightmare if access controls aren't properly configured. Unauthorized users can quickly exploit weak authentication and overly permissive policies.

In this project, I explored AWS Identity and Access Management (IAM) to understand how to manage users, groups, and permissions securely. I created a custom password policy, examined pre‑created IAM users and groups, attached policies to groups, and tested access levels for different roles. The goal was to see firsthand how IAM enforces the principle of least privilege—giving users only the permissions they need to perform their jobs.

---

### Objectives

#### After completing this project, I was able to:
- Create and apply an IAM password policy
- Explore pre‑created IAM users and user groups
- Inspect IAM policies attached to user groups
- Add users to groups with specific capabilities
- Locate and use the IAM sign‑in URL
- Experiment with the effects of policies on service access

---

 ### Task 1: Create an Account Password Policy
 
I started by opening the AWS Management Console and noting the Region displayed in the upper‑right corner (Oregon). Then I searched for IAM in the search bar and selected it

<img width="932" height="550" alt="Screenshot (210)" src="https://github.com/user-attachments/assets/704c91e2-afdd-42ae-bc8d-d58aada1b946" />

In the left navigation pane, I clicked Account settings. There I saw the default password policy that was currently in effect for the account. To strengthen it, I clicked the Change password policy button.

<img width="1338" height="553" alt="Screenshot (211)" src="https://github.com/user-attachments/assets/686fe5d0-9d58-4366-808d-135b46acc572" />

--

<img width="1119" height="338" alt="Screenshot (213)" src="https://github.com/user-attachments/assets/0349b3b1-400e-43f5-975f-0abe05911200" />

I configured the following options:
- Enforce minimum password length: I changed it from 8 to 10 characters.
- Require at least one uppercase letter: I checked this box.
- Require at least one lowercase letter: I checked this box.
- Require at least one number: I checked this box.
- Require at least one non‑alphanumeric character: I checked this box.
- Enable password expiration: I left the default of 90 days.
- Prevent password reuse: I left the default of 5 passwords.
- #### I made sure to leave Password expiration requires administrator reset unchecked.

  
<img width="1340" height="488" alt="Screenshot (214)" src="https://github.com/user-attachments/assets/1caeab58-2a77-459a-ae46-748c1a947e9b" />

--


<img width="1334" height="522" alt="Screenshot (216)" src="https://github.com/user-attachments/assets/81bc189e-7cf2-4eab-845c-7e6e9db9b5be" />

After confirming my selections, I clicked Save changes.


<img width="1121" height="366" alt="Screenshot (217)" src="https://github.com/user-attachments/assets/851cecca-95d2-4d4d-a0b0-aac573bea6ed" />

#### A strong password policy is the first line of defense against unauthorised access. By enforcing complexity, length, and rotation rules across all IAM users, I reduced the risk of brute‑force attacks and credential stuffing. This policy applies globally to every user in the AWS account, ensuring consistent security hygiene
