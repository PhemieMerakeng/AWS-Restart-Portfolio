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

 ## Task 1: Create an Account Password Policy
 
I started by opening the AWS Management Console and noting the Region displayed in the upper‑right corner (Oregon). Then I searched for IAM in the search bar and selected it

<img width="932" height="550" alt="Screenshot (210)" src="https://github.com/user-attachments/assets/704c91e2-afdd-42ae-bc8d-d58aada1b946" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

In the left navigation pane, I clicked Account settings. There I saw the default password policy that was currently in effect for the account. To strengthen it, I clicked the edit password policy button.

<img width="1338" height="553" alt="Screenshot (211)" src="https://github.com/user-attachments/assets/686fe5d0-9d58-4366-808d-135b46acc572" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

<img width="1119" height="338" alt="Screenshot (213)" src="https://github.com/user-attachments/assets/0349b3b1-400e-43f5-975f-0abe05911200" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

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

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:


<img width="1334" height="522" alt="Screenshot (216)" src="https://github.com/user-attachments/assets/81bc189e-7cf2-4eab-845c-7e6e9db9b5be" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

After confirming my selections, I clicked Save changes.

<img width="1121" height="366" alt="Screenshot (217)" src="https://github.com/user-attachments/assets/851cecca-95d2-4d4d-a0b0-aac573bea6ed" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

### 💡 A strong password policy is the first line of defense against unauthorised access. By enforcing complexity, length, and rotation rules across all IAM users, I reduced the risk of brute‑force attacks and credential stuffing. This policy applies globally to every user in the AWS account, ensuring consistent security hygiene

---

## Task 2: Explore Users and User Groups

### :hammer_and_wrench: Inspecting the IAM Users

I went back to the left navigation pane and clicked Users. I saw three pre‑created IAM users: user-1, user-2, and user-3.

<img width="1366" height="375" alt="Screenshot (218)" src="https://github.com/user-attachments/assets/876f099f-47e5-42c5-b67e-a827fbf8290c" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

 I clicked on user-1 to view its details. On the Summary page, I looked at the Permissions tab and saw that no permissions were attached

<img width="1345" height="517" alt="Screenshot (219)" src="https://github.com/user-attachments/assets/29813cfb-ac47-4a61-85be-f2527778039a" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Then I clicked the Groups tab and noticed that user-1 was not a member of any group

<img width="1366" height="551" alt="Screenshot (220)" src="https://github.com/user-attachments/assets/903f5ca9-5012-4a49-87cb-73d9c1dda85e" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

 I checked the Security credentials tab and confirmed that a console password had been assigned.

 <img width="1366" height="441" alt="Screenshot (221)" src="https://github.com/user-attachments/assets/230d71a0-5707-4c75-bcc0-001f4b87bfcd" />

 :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

#### Next, I returned to the Users list and clicked user-2. I repeated the same inspection: no permissions, no group membership, but a console password present

 #### I did the same for user-3 and found the same situation

 ### :hammer_and_wrench: Inspecting the IAM User Groups
 
After examining the users, I clicked User groups in the left navigation. I saw three groups: __EC2-Admin, EC2-Support, and S3-Support__. All did not have any assigned users. 

<img width="1366" height="536" alt="Screenshot (222)" src="https://github.com/user-attachments/assets/6d35e33e-b8c1-405f-9d03-6afcbadbf7d5" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

I clicked on the the EC2-Support group. 

<img width="1366" height="509" alt="Screenshot (223)" src="https://github.com/user-attachments/assets/6af31bca-960d-4b3f-9783-ac914b368a22" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

 I went to the Permissions tab, where I saw a managed policy named AmazonEC2ReadOnlyAccess. I expanded it by clicking the small triangle next to the policy name. The JSON policy showed that it allowed Describe actions on EC2, Elastic Load Balancing, CloudWatch, and Auto Scaling.

 <img width="1366" height="530" alt="Screenshot (224)" src="https://github.com/user-attachments/assets/c8f6bc31-8a4b-4343-8188-e26c378f0d8e" />

 :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

 <img width="1366" height="528" alt="Screenshot (225)" src="https://github.com/user-attachments/assets/4605e543-2d05-4d0e-b448-475fc9870e4a" />

 :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

 Then I went back to the User groups list and clicked S3-Support
 
<img width="1366" height="569" alt="Screenshot (227)" src="https://github.com/user-attachments/assets/7ca30bca-36c8-49e0-9ea8-0c929d47603d" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Under Permissions, I expanded the attached managed policy AmazonS3ReadOnlyAccess. This policy allowed Get and List actions on Amazon S3.

<img width="1366" height="568" alt="Screenshot (228)" src="https://github.com/user-attachments/assets/347ab18f-2f5a-49d5-b350-c31a2e2fd6e0" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Finally, I clicked EC2-Admin. In the Permissions tab, ___I noticed that instead of a managed policy, this group had a customer inline policy named EC2-Admin-Policy. Expanding it showed permissions to Describe EC2 resources, plus the specific actions StartInstances and StopInstances__

<img width="1366" height="572" alt="Screenshot (229)" src="https://github.com/user-attachments/assets/127afc05-3393-49e8-a457-39e7bcb5c3e7" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

### 💡 This exploration showed me the initial state of the IAM environment: all three users started with no permissions and belonged to no groups. Understanding this baseline is essential before assigning rights. Then, by examining the groups and their attached policies, I learned how permissions are organised and the difference between managed policies (reusable, maintained by AWS) and inline policies (one‑off, attached directly to a single group). Grouping users with common job functions and attaching appropriate policies is the foundation of efficient access management.

---

## Task 3: Add Users to User Groups
To assign these permissions, I added each user to the appropriate group.

I started by clicking User groups in the left navigation

<img width="1366" height="536" alt="Screenshot (222)" src="https://github.com/user-attachments/assets/69e81062-4a8f-46f4-98ee-37a8783d36b5" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Then clicked the __S3-Support group__. Under the Users tab, I clicked Add users.

<img width="1366" height="571" alt="Screenshot (230)" src="https://github.com/user-attachments/assets/d124c116-50a4-4b1f-8b08-043e2001fdd7" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

In the window that appeared, I selected the check box for user-1 and clicked Add users

<img width="1366" height="575" alt="Screenshot (231)" src="https://github.com/user-attachments/assets/aa55feb6-7d33-4601-8aff-6986411ff08e" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

After a moment a confirmation pop up showing a user was added to the group

<img width="1366" height="476" alt="Screenshot (232)" src="https://github.com/user-attachments/assets/486fd125-96b5-4001-a317-a555d80011d0" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Next, I returned to User groups, __clicked EC2-Support__, went to the Users tab, and clicked Add users. I selected user-2 and added them.

<img width="1366" height="297" alt="Screenshot (233)" src="https://github.com/user-attachments/assets/0ccf3bc7-7a9d-4593-bc9d-b7454b41d54f" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

<img width="1133" height="445" alt="Screenshot (234)" src="https://github.com/user-attachments/assets/715c5208-0d5c-4c08-8170-d7cc04819632" />

Finally, I repeated the process for the __EC2-Admin group__, adding user-3.

<img width="1366" height="313" alt="Screenshot (235)" src="https://github.com/user-attachments/assets/4b281b96-f856-4d48-832a-a030b7e117d6" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

__To confirm, I went back to the main User groups page. Each group now displayed a 1 in the Users column, indicating that all three users had been successfully added__

<img width="1139" height="309" alt="Screenshot (237)" src="https://github.com/user-attachments/assets/56b0a569-5382-476f-9a5d-82cb0be6264e" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

### 💡 Assigning permissions through groups is a best practice in IAM. It’s much easier to manage a handful of groups than dozens of individual user permissions. If a user changes roles, I can simply move them to a different group instead of rewriting policies. This approach also enforces the principle of least privilege by ensuring users only inherit the permissions needed for their job

---

## Task 4: Sign In and Test User Permissions

### 🛠️ Obtaining the IAM Sign‑in URL

I clicked Dashboard in the left navigation. Under AWS Account, I located the Sign‑in URL for IAM users in this account I copied it to a text editor for easy access.

<img width="364" height="209" alt="Screenshot (238)" src="https://github.com/user-attachments/assets/41d41e07-1fe3-4aeb-b163-54ea22fcaeea" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

### 🛠️ Testing user-1 (S3 Support)

I opened a private/incognito browser windowI and pasted the sign‑in URL into the address bar and pressed Enter.
I signed in with:
- IAM user name: user-1
- Password: Lab-Password1

  <img width="1036" height="555" alt="Screenshot (239)" src="https://github.com/user-attachments/assets/ce2ab95f-7efb-4b6d-810d-8ae972bc755b" />

  :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

From the Services menu, I selected S3

<img width="934" height="542" alt="Screenshot (241)" src="https://github.com/user-attachments/assets/65c531d8-6654-4198-80aa-54f440fbed32" />

  :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:
  
could see a list of S3 buckets. I clicked on one of the buckets and browsed its contents—read‑only access worked as expected.

<img width="1063" height="312" alt="Screenshot (242)" src="https://github.com/user-attachments/assets/5f25a1bc-0340-44d3-95d2-53fa7ac5a0c7" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Then I switched to EC2 by selecting it from the Services menu and clicked Instances in the left navigation. I received an error message: You are not authorized to perform this operation. This confirmed that user-1 had no EC2 permissions.

<img width="1118" height="261" alt="Screenshot (243)" src="https://github.com/user-attachments/assets/d5d43dc0-bef9-45c0-a6e8-9936381b8e53" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

I signed out by clicking user-1 at the top‑right and choosing Sign out.

<img width="1111" height="568" alt="Screenshot (244)" src="https://github.com/user-attachments/assets/1ccc8731-8e49-4593-8f75-fc047588106e" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

### ⚒️ Testing user-2 (EC2 Support)
In the same private window, I pasted the sign‑in URL again and signed in as __user-2 with password Lab-Password2__

<img width="1033" height="515" alt="Screenshot (245)" src="https://github.com/user-attachments/assets/2cf2b6a8-255c-41b6-8421-182707bdafc9" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

I went to Services → EC2 → Instances. I could see the EC2 instance details

<img width="936" height="548" alt="Screenshot (246)" src="https://github.com/user-attachments/assets/0f30ac3a-c31d-4622-9aaa-2dc8963998b0" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

<img width="1121" height="201" alt="Screenshot (248)" src="https://github.com/user-attachments/assets/57d271f9-8743-4ed3-ae77-9a22b2601739" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

I selected the instance by checking the box next to it, then clicked the Instance state dropdown and chose Stop instance. In the confirmation dialog, I clicked Stop. __An error appeared: Failed to stop the instance. You are not authorized to perform this operation. This showed that while read‑only worked, write actions were blocked.__

<img width="1104" height="226" alt="Screenshot (249)" src="https://github.com/user-attachments/assets/38ba84a6-1882-445d-93b7-b44002cfebd9" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

<img width="1070" height="252" alt="Screenshot (250)" src="https://github.com/user-attachments/assets/a40189b0-8140-4694-84e1-ca2387989f41" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Next, I tried Services → S3. __I received a message: You don't have permissions to list buckets. This confirmed that user-2 had no S3 access.__

<img width="1077" height="372" alt="Screenshot (254)" src="https://github.com/user-attachments/assets/9526ee8e-b488-497c-a247-818e1028cd06" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:


### ⚒️ Testing user-3 (EC2 Admin)

I pasted the sign‑in URL once more and signed in __as user-3 with password Lab-Password3.__

I navigated to EC2 → Instances, selected the instance, clicked Instance state → Stop instance, and confirmed by clicking Stop

<img width="1118" height="248" alt="Screenshot (256)" src="https://github.com/user-attachments/assets/eefe0ef6-0e0b-4e30-874c-1dff1346f361" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

This time the instance successfully entered the stopping state. This verified that user-3 had the full EC2 admin permissions.

<img width="1109" height="239" alt="Screenshot (259)" src="https://github.com/user-attachments/assets/b0a92937-8d58-4843-9b26-f33b649dc5bf" />

:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

This hands‑on verification confirmed that the policies were working exactly as designed. It demonstrated:
- Read‑only access for support roles (they can troubleshoot but not change resources).
- Deny by default – users had no access to services not explicitly allowed.
- Elevated permissions for administrators to perform operational tasks.

### Testing permissions in this way is crucial to ensure that the security model behaves as expected and that no accidental over‑privileging has occurred.

---

## Conclusion

🌐 Through this project, I successfully:
- Created and applied a custom password policy to strengthen account security.
- Explored IAM users, groups, and the differences between managed and inline policies.
- Added users to groups based on their job functions, following the principle of least privilege.
- Used the IAM sign‑in URL to test access levels for each user.
- Verified that policies correctly restricted or allowed actions on EC2 and S3.

IAM is the foundation of security in AWS. By mastering its core concepts—users, groups, policies, and password policies—I can now design and audit access control systems that protect cloud resources while enabling productivity. This lab was a practical step toward understanding how identity and permissions work in a real‑world AWS environment.











 







