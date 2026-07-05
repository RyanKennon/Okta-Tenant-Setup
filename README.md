<p align="center">
  <img width="900" height="500" alt="image" src="https://github.com/user-attachments/assets/2c068a6c-d82b-4a43-ad32-d9fe559e1837" />
</p>

# Okta Tenant Setup & Configuration — Identity Provider Foundations Lab

This project demonstrates the foundational configuration of an Okta Identity Provider (IdP) tenant from the ground up, simulating the initial setup responsibilities of an IAM Analyst or Identity Engineer in an enterprise environment. Starting with org initialization and brand customization, the lab walks through building a production-ready Okta org for a fictional company, Kennon Technologies, including custom profile attribute design, user identity creation, group structure, dynamic group rule automation, authentication policy configuration, global session management, and authenticator enrollment policy enforcement. All configurations are hands-on in a live Okta trial org and reflect real-world IAM practices around identity lifecycle management, access policy design, and directory administration. The lab serves as the foundational layer for subsequent Okta labs covering Active Directory integration, SAML SSO, SCIM provisioning, lifecycle automation, and access governance.

---

## Environments and Technologies Used

- Okta Identity Cloud (Trial Org)
- Okta Admin Console
- Okta Universal Directory
- Okta Profile Editor
- Okta Group Rules & Expression Language
- Okta Authentication Policies
- Okta Global Session Policy
- Okta Authenticator Enrollment Policy

---

## Table of Contents

- [1) Organization Initialization](#1-organization-initialization)
- [2) Branding](#2-branding)
- [3) Create User Identities](#3-create-a-user-identities)
- [4) Add Custom Profile Attributes](#4-add-custom-profile-attributes)
- [5) Update Attributes on User Identities](#5-update-attributes-on-user-identities)
- [6) Create Groups](#6-create-groups)
- [7) Manually Assign Users to a Group](#7-manually-assign-users-to-a-group)
- [8) Create Group Rules to Assign Users to Groups](#8-create-group-rules-to-assign-users-to-groups)
- [9) Create an Authentication Policy](#9-create-an-authentication-policy)
- [10) Add Rules to a Policy](#10-add-rules-to-a-policy)
- [11) Create a Global Session Policy and Configure Rule](#11-create-a-global-session-policy-and-configure-rule)
- [12) Create an Authenticator Enrollment Policy and Configure Enrollment Rule](#12-create-an-authenticator-enrollment-policy-and-configure-enrollment-rule)

---

### 1) Organization Initialization

Organization initialization configures the foundational identity of the Okta 
org including the company name, contact information, and address. These settings 
appear in Okta-generated emails and audit logs and establish the org as belonging 
to Kennon Technologies.

1.  In the **Okta Admin Console** open the **Settings** tab then select **Account**
2.  In the **Organization Contact** section select **Edit**
3.  Fill out the the company information with the following information:
   - **Company Name:** Kennon Technologies
   - **Telephone Number:** 999-999-9999
   - **Address:** 100 1st Street
   - **City:** Fort Worth
   - **State:** Texas
   - **Zip Code:** 76107
   - **Country:** United States of America

4. **Save**

<p align="center">
  <img width="464" height="630" alt="image" src="https://github.com/user-attachments/assets/a8f31d1e-c2d8-4bc6-914a-93d3df55d09f" />
</p>

---

### 2) Branding

Branding customizes the visual identity of the Okta org by uploading a company 
logo, setting a primary color, and configuring a favicon. This ensures users 
interact with a sign-in experience that reflects Kennon Technologies rather than 
a generic Okta tenant.

1. Open the **Customizations** tab then select **Branding** then select **Create Brand**
2. On the **Theme** page make the following changes:
   - **Logo:** [Kennon Technologies Logo](https://github.com/RyanKennon/Okta-Tenant-Setup/blob/main/Kennon-Technologies-Logo.png)
   - **Primary Color:** #1800AD
   - **Favicon:** [Kennon Technologies Favicon](https://github.com/RyanKennon/Okta-Tenant-Setup/blob/main/KT-Favicon.png)

3. **Save**

<p align="center">
  <img width="517" height="616" alt="image" src="https://github.com/user-attachments/assets/5a21bf25-724c-4108-83c2-deca9c8a0cec" />
</p>

4. On the **Pages** tab select **Configure** on the **Sign-In Page**
5. Check the **Solid Background** option then **Save and Publish**

<p align="center">
  <img width="1383" height="749" alt="image" src="https://github.com/user-attachments/assets/a10378b3-d9d3-4446-86c4-3d590b2dcf25" />
</p>

6. Do the same for the **End-User Dashboard** and the **Error Pages**

<p align="center">
  <img width="1379" height="448" alt="image" src="https://github.com/user-attachments/assets/b321f1f0-143a-4919-b10f-9d59360d2da9" />
</p>

---

### 3) Create a User Identities

User identities represent individual employees in the Okta Universal Directory. 
Creating user accounts with accurate profile information establishes the foundation 
for group membership, application access, and lifecycle management throughout 
the lab.

1. Open the **Directory** tab then select **People** then select **Add Person**
2. Create a User Identity with the following information
   - **First Name:** John
   - **Last Name:** Smith
   - **Username:** john.smith@kennontech.com
   - **Primary Email:** john.smith@kennontech.com
   - **I Will Set Password:** Checked
   - **Password:** WorldCup2026!
   - **User Must Change Password on First Login:** Checked
  
3. **Save and Add Another**
  
<p align="center">
  <img width="693" height="837" alt="image" src="https://github.com/user-attachments/assets/ae569976-4027-4cb2-9b14-9f8081daa1bb" />
</p>

4. Create a second User Identity with the following information:
   - **First Name:** Jane
   - **Last Name:** Doe
   - **Username:** jane.doe@kennontech.com
   - **Primary Email:** jane.doe@kennontech.com
   - **I Will Set Password:** Checked
   - **Password:** WorldCup2026!
   - **User Must Change Password on First Login:** Checked

5. **Save and Add Another**

<p align="center">
  <img width="692" height="829" alt="image" src="https://github.com/user-attachments/assets/fdf727bc-9be5-4b13-b402-e8706a9cb718" />
</p>

6. Create a third User Identity with the following information:
   - **First Name:** Bob
   - **Last Name:** Johnson
   - **Username:** bob.johnson@kennontech.com
   - **Primary Email:** bob.johnson@kennontech.com
   - **I Will Set Password:** Checked
   - **Password:** WorldCup2026!
   - **User Must Change Password on First Login:** Checked

7. **Save**

<p align="center">
  <img width="693" height="831" alt="image" src="https://github.com/user-attachments/assets/5bdde775-d81b-4096-8f02-346f931fe384" />
</p>


---

### 4) Add Custom Profile Attributes

Custom profile attributes extend the default Okta user schema to capture 
organization-specific data that doesn't exist in the standard profile. These 
attributes can be used for reporting, group rule logic, and attribute mapping 
to downstream applications.

1. Open the **Directory** then **Profile Editor** then select **User (default)**
2. Select **Add Attribute** then create an Attribute with the following information:
   - **Data Type:** String
   - **Display Name:** Employee ID
   - **Variable Name:** employeeID
   - **Description:** Unique HR System Identifier
   - **User Description:** Hide

<p align="center">
  <img width="682" height="915" alt="image" src="https://github.com/user-attachments/assets/f948f092-03d8-4d5b-a424-fc42a0f8c212" />
</p>

3. **Save and Add Another**
4. Create a Second Attribute with the following information:
   - **Data Type:** String
   - **Display Name:** Start Date
   - **Variable Name:** startDate
   - **Description:** The User's Employment Start Date
   - **User Description:** Read Only

<p align="center">
  <img width="685" height="871" alt="image" src="https://github.com/user-attachments/assets/c31fff04-cc1d-4f1e-9f0b-1ae809b26360" />
</p>

5. **Save**

---

### 5) Update Attributes on User Identities

Populating custom attributes on user identities validates that the new schema 
fields are functioning correctly and ensures each user has accurate department, 
employee ID, and start date information that will drive downstream group 
assignment and access decisions.

1. Open the **Directory** then **People**
2. Select **John Smith** then the **Profile** tab then click **Edit**
3. Find the **Attributes** and enter the following Attribute information:
   - **Department:** Finance
   - **Employee ID:** EMP-00057
   - **Start Date:** 2026-03-26

5. **Save**

<p align="center">
  <img width="727" height="424" alt="image" src="https://github.com/user-attachments/assets/0981b9b8-94bb-4cea-9cb8-3b5ab387064e" />
</p>

6. For **Jane Doe** make and save the following attribute information:
   - **Department:** IT
   - **Employee ID:** EMP-00017
   - **Start Date:** 2024-01-17
  
<p align="center">
  <img width="705" height="425" alt="image" src="https://github.com/user-attachments/assets/8996250f-4837-4cbe-985b-895cfbbb5d87" />
</p>

7. For **Bob Johnson** make and save the following attribute information:
   - **Department:** Human Resources
   - **Employee ID:** EMP-00012
   - **Start Date:** 2023-06-12

<p align="center">
  <img width="693" height="412" alt="image" src="https://github.com/user-attachments/assets/0028ab02-2449-4551-bdbe-caa7f3115931" />
</p>

---

### 6) Create Groups

Groups in Okta are used to organize users and control access to applications 
and policies. Creating department-based groups establishes the access structure 
that will be used to assign application access, session policies, and 
authenticator enrollment requirements.

1. Open the **Directory** tab then select **Groups** then select **Add Group**
2. Create a Group using the following information:
   - **Name:** Kennon Technologies Employees
   - **Description:** Standard Kennon Technologies Employees

3. **Save**

<p align="center">
  <img width="687" height="255" alt="image" src="https://github.com/user-attachments/assets/3235e97c-0b36-4863-8467-732d4aab70c7" />
</p>

4. Create 3 additional groups named: 
   - **Finance**
   - **IT**
   - **Human Resources**

---

### 7) Manually Assign Users to a Group

Manually assigning users to the Kennon Technologies Employees group demonstrates 
direct group membership management and establishes the base group that will be 
referenced in the Global Session Policy and Authenticator Enrollment Policy 
configurations.

1. Open the **Directory** tab then select **Groups**
2. Select **Kennon Technologies Employees** and open the **People** tab
3. Select **Assign People**
4. Find **John Smith, Jane Doe, and Bob Johnson** then press the **+** next to their names
5. **Done**

<p align="center">
  <img width="1018" height="429" alt="image" src="https://github.com/user-attachments/assets/1719c8c0-517f-4b76-aff4-4827a3878780" />
</p>

---

### 8) Create Group Rules to Assign Users to Groups

Group rules use Okta Expression Language to automatically assign users to groups 
based on their profile attribute values. This eliminates the need for manual 
group management and ensures users are always placed in the correct department 
group as their profile information changes.

1. Open the **Directory** tab then select **Groups**
2. Select the **Rules** tab then select **Add Rule**
3. Create a Group Rule with the following information:
   - **Rule Name:** Assign Finance Users
   - **If:** User Attribute Department Equals Finance
   - **Assign To:** Finance
  
4. **Save**

<p align="center">
  <img width="989" height="449" alt="image" src="https://github.com/user-attachments/assets/2e467df1-1e99-4e2f-8612-b49574ee9a7e" />
</p>

5. To the Right of the **Assign Finance Users** rule select **Actions** then select **Activate**

<p align="center">
  <img width="999" height="477" alt="image" src="https://github.com/user-attachments/assets/dd5dad06-e4e8-4407-bb38-0c2f2f35a2f8" />
</p>


6. Create a second Group Rule with the following information:
   - **Rule Name:** Assign IT Users
   - **If:** User Attribute Department Equals IT
   - **Assign To:** IT
  
7. **Save** and **Activate** the rule

<p align="center">
  <img width="989" height="448" alt="image" src="https://github.com/user-attachments/assets/6ad1d8a2-6c0d-4246-bd69-45e150c3c628" />
</p>

8. Create a third Group Rule with the following information:
   - **Rule Name:** Assign Human Resources Users
   - **If:** User Attribute Department Equals Human Resources
   - **Assign To:** Human Resources

9. **Save** and **Activate** the rule

<p align="center">
  <img width="993" height="455" alt="image" src="https://github.com/user-attachments/assets/a8e57c99-5875-4d26-88e0-67afabad7f7c" />
</p>

---

### 9) Create an Authentication Policy

Authentication policies define the security requirements users must meet to 
access applications assigned to that policy. Creating a dedicated policy for 
Kennon Technologies employees establishes a baseline access control layer 
separate from Okta's default policy.

1. Open the **Security** tab then go to **Authentication Policies**
2. Select **App Sign-In** then **Create Policy**
3. Create an Authentication Policy with the following information:
   - **Name:** Standard Employee Policy
   - **Description:** Requires MFA for All Employees

4. **Create Policy**

<p align="center">
  <img width="483" height="361" alt="image" src="https://github.com/user-attachments/assets/6b84bb9e-2efe-4e3e-9484-25e63809b178" />
</p>

---

### 10) Add Rules to a Policy

Authentication policy rules define the specific factor requirements users must 
satisfy under different conditions. Configuring a password-only rule and an MFA 
rule demonstrates how Okta evaluates rules in priority order and applies the 
first matching rule to the authentication request.

1. With the **Standard Employee Policy** open select **Add Rule**
2. For the First Rule enter the following information:
   - **Rule Name:** Password Only
   - **Then Access Is:** Allowed After Successful Authentication
   - **And User Must Authenticate With:** Password

<p align="center">
  <img width="913" height="138" alt="image" src="https://github.com/user-attachments/assets/ad9330db-5166-4b16-b24d-ce332977c4af" />
</p>

3. **Save** then **Add Rule** again
4. For the Second Rule enter the following information:
  - **Rule Name:** Require MFA
  - **Then Access Is:** Allowed After Successful Authentication
  - **And User Must Authenticate With:** Password + Another Factor

<p align="center">
  <img width="869" height="138" alt="image" src="https://github.com/user-attachments/assets/14b3ca10-f7fc-4e66-8525-c00d6603790b" />
</p>

5. **Save**

---

### 11) Create a Global Session Policy and Configure Rule

The Global Session Policy controls how long a user's Okta session remains active 
across all applications. Configuring session lifetime and idle timeout settings 
ensures that inactive sessions are terminated automatically, reducing the risk 
of unauthorized access from unattended devices.

1. Open the **Security** tab then select **Global Session Policy** then select **Add Policy**
2. Create a Global Session Policy with the following information:
   - **Policy Name:** Standard Session Policy
   - **Description:** Standard Session Settings for Kennon Technologies Employees
   - **Assign to Groups:** Kennon Technologies Employees
  
3. **Create Policy and Add Rule**

<p align="center">
  <img width="590" height="423" alt="image" src="https://github.com/user-attachments/assets/76bb23de-36c3-408a-b8f8-ed78801c62dc" />
</p>

4. For the Global Session Policy Rule enter the following information
   - **Rule Name:** Standard Session Rule
   - **Maximum Okta Session Lifetime:** 8 Hours
   - **Maximum Idle Time:** 2 Hours
   - **Persist Session Cookies:** Disable
  
5. **Create Rule**

<p align="center">
  <img width="873" height="582" alt="image" src="https://github.com/user-attachments/assets/75f9d352-1d7f-4b65-8b45-f824979188ab" />
</p>

---

### 12) Create an Authenticator Enrollment Policy and Configure Enrollment Rule

Authenticator enrollment policies control which authentication methods users are 
permitted to enroll in and under what conditions. Configuring a dedicated 
enrollment policy for Kennon Technologies employees ensures that authenticator 
registration is governed by organizational policy rather than left to individual 
user preference.

1. Open the **Security** tab then select **Authenticators**
2. Select the **Enrollments** tab then select **Add a Policy**
3. Create an Authenticator Enrollment Policy with the following information:
   - **Policy Name:** Employee Enrollment Policy
   - **Description:** Authenticator Enrollment Requirements for Kennon Technologies Employees
   - **Assign to Groups:** Kennon Technologies Employees
  
4. **Create Policy**

<p align="center">
  <img width="593" height="903" alt="image" src="https://github.com/user-attachments/assets/a61e6ae0-49c0-4e6c-a59a-9028ece63f68" />
</p>

5. For the Authenticator Enrollment Rule enter the following information:
   - **Rule Name:** Employee Enrollment Rule
   - **If User's IP is:** Anywhere
   - **And User is Accessing:** Check Okta and Applications and Any Specific Application the Supports MFA Enrollment
   - **Then Enrollment is:** Allowed for All Authenticators
  
6. **Create Rule**

<p align="center">
  <img width="905" height="773" alt="image" src="https://github.com/user-attachments/assets/a734641c-ae99-4ff1-b02a-c7ed23dc9d44" />
</p>
