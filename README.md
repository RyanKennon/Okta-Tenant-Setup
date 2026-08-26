<p align="center">
  <img src="Images/Header.png" img width="900" height="500" alt="image">
</p>

# Okta Tenant Setup & Configuration

This project demonstrates the foundational configuration of an Okta Identity Provider (IdP) tenant from the ground up, simulating the initial setup responsibilities of an IAM Analyst or Identity Engineer in an enterprise environment. Starting with org initialization and brand customization, the lab walks through building a production-ready Okta org for a fictional company, Kennon Technologies, including custom profile attribute design, user identity creation, group structure, dynamic group rule automation, authentication policy configuration, global session management, and authenticator enrollment policy enforcement. All configurations are hands-on in a live Okta trial org and reflect real-world IAM practices around identity lifecycle management, access policy design, and directory administration. The lab serves as the foundational layer for subsequent Okta labs covering Active Directory integration, SAML SSO, SCIM provisioning, lifecycle automation, and access governance.

---

## Prerequisites

This is the first lab of the [Okta IAM Lab Series](https://github.com/RyanKennon/Okta-Lab-Series/tree/main). 
The following are required before starting the series:

- **Okta Trial Org** — Sign up for a free Okta trial org at [developer.okta.com](https://developer.okta.com)
- **GitHub Account** — Required to follow along with lab documentation and host your own portfolio

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
- [8) Create Group Rules](#8-create-group-rules)
- [9) Create an Authentication Policy](#9-create-an-authentication-policy)
- [10) Create a Global Session Policy](#10-create-a-global-session-policy)
- [11) Create an Authenticator Enrollment Policy](#11-create-an-authenticator-enrollment-policy)

---

### 1) Organization Initialization

Organization initialization configures the foundational identity of the Okta 
org including the company name, contact information, and address. These settings 
appear in Okta-generated emails and audit logs and establish the org as belonging 
to Kennon Technologies.

1.  In the **Okta Admin Console** open the **Settings** tab then select **Account**
2.  In the **Organization Contact** section select **Edit**
3.  Fill out the company information with the following information:
   - **Company Name:** Kennon Technologies
   - **Telephone Number:** 999-999-9999
   - **Address:** 100 1st Street
   - **City:** Fort Worth
   - **State:** Texas
   - **Zip Code:** 76107
   - **Country:** United States of America

4. **Save**

<p align="center">
  <img src="Images/Image%201.png" img width="464" height="630" alt="image">
</p>

---

### 2) Branding

Branding customizes the visual identity of the Okta org by uploading a company 
logo, setting a primary color, and configuring a favicon. This ensures users 
interact with a sign-in experience that reflects Kennon Technologies rather than 
a generic Okta tenant.

1. Open the **Customizations** tab then select **Brands** then select **Create Brand**
2. On the **Theme** page make the following changes:
   - **Logo:** [Kennon Technologies Logo](https://github.com/RyanKennon/Okta-Tenant-Setup/blob/main/Assets/Kennon-Technologies-Logo.png)
   - **Primary Color:** #1800AD
   - **Favicon:** [Kennon Technologies Favicon](https://github.com/RyanKennon/Okta-Tenant-Setup/blob/main/Assets/KT-Favicon.png)

3. **Save**

<p align="center">
  <img src="Images/Image%202.png" img width="517" height="616" alt="image">
</p>

4. On the **Pages** tab select **Configure** on the **Sign-In Page**
5. Check the **Solid Background** option then **Save and Publish**

<p align="center">
  <img src="Images/Image%203.png" img width="1383" height="749" alt="image">
</p>

6. Do the same for the **End-User Dashboard** and the **Error Pages**

<p align="center">
  <img src="Images/Image%204.png" img width="1379" height="448" alt="image">
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
  <img src="Images/Image%205.png" img width="693" height="837" alt="image">
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
  <img src="Images/Image%206.png" img width="692" height="829" alt="image">
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
  <img src="Images/Image%207.png" img width="693" height="831" alt="image">
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
  <img src="Images/Image%208.png" img width="682" height="915" alt="image">
</p>

3. **Save and Add Another**
4. Create a Second Attribute with the following information:
   - **Data Type:** String
   - **Display Name:** Start Date
   - **Variable Name:** startDate
   - **Description:** The User's Employment Start Date
   - **User Description:** Read Only

<p align="center">
  <img src="Images/Image%209.png" img width="685" height="871" alt="image">
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
  <img src="Images/Image%2010.png" img width="727" height="424" alt="image">
</p>

6. For **Jane Doe** make and save the following attribute information:
   - **Department:** IT
   - **Employee ID:** EMP-00017
   - **Start Date:** 2024-01-17
  
<p align="center">
  <img src="Images/Image%2011.png" img width="705" height="425" alt="image">
</p>

7. For **Bob Johnson** make and save the following attribute information:
   - **Department:** Human Resources
   - **Employee ID:** EMP-00012
   - **Start Date:** 2023-06-12

<p align="center">
  <img src="Images/Image%2012.png" img width="693" height="412" alt="image">
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
  <img src="Images/Image%2013.png" img width="687" height="255" alt="image">
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
  <img src="Images/Image%2014.png" img width="1018" height="429" alt="image">
</p>

---

### 8) Create Group Rules

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
  <img src="Images/Image%2015.png" img width="989" height="449" alt="image">
</p>

5. To the Right of the **Assign Finance Users** rule select **Actions** then select **Activate**

<p align="center">
  <img src="Images/Image%2016.png" img width="999" height="477" alt="image">
</p>


6. Create a second Group Rule with the following information:
   - **Rule Name:** Assign IT Users
   - **If:** User Attribute Department Equals IT
   - **Assign To:** IT
  
7. **Save** and **Activate** the rule

<p align="center">
  <img src="Images/Image%2017.png" img width="989" height="448" alt="image">
</p>

8. Create a third Group Rule with the following information:
   - **Rule Name:** Assign Human Resources Users
   - **If:** User Attribute Department Equals Human Resources
   - **Assign To:** Human Resources

9. **Save** and **Activate** the rule

<p align="center">
  <img src="Images/Image%2018.png" img width="993" height="455" alt="image">
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
  <img src="Images/Image%2019.png" img width="483" height="361" alt="image">
</p>

5. With the **Standard Employee Policy** open select **Add Rule**
6. For the First Rule enter the following information:
   - **Rule Name:** Password Only
   - **Then Access Is:** Allowed After Successful Authentication
   - **And User Must Authenticate With:** Password

<p align="center">
  <img src="Images/Image%2020.png" img width="913" height="138" alt="image">
</p>

7. **Save** then **Add Rule** again
8. For the Second Rule enter the following information:
  - **Rule Name:** Require MFA
  - **Then Access Is:** Allowed After Successful Authentication
  - **And User Must Authenticate With:** Password + Another Factor

<p align="center">
  <img src="Images/Image%2021.png" img width="869" height="138" alt="image">
</p>

9. **Save**

---

### 10) Create a Global Session Policy

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
  <img src="Images/Image%2022.png" img width="590" height="423" alt="image">
</p>

4. For the Global Session Policy Rule enter the following information
   - **Rule Name:** Standard Session Rule
   - **Maximum Okta Session Lifetime:** 8 Hours
   - **Maximum Idle Time:** 2 Hours
   - **Persist Session Cookies:** Disable
  
5. **Create Rule**

<p align="center">
  <img src="Images/Image%2023.png" img width="873" height="582" alt="image">
</p>

---

### 11) Create an Authenticator Enrollment Policy

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
  <img src="Images/Image%2024.png" img width="593" height="903" alt="image">
</p>

5. For the Authenticator Enrollment Rule enter the following information:
   - **Rule Name:** Employee Enrollment Rule
   - **If User's IP is:** Anywhere
   - **And User is Accessing:** Check Okta and Applications and Any Specific Application the Supports MFA Enrollment
   - **Then Enrollment is:** Allowed for All Authenticators
  
6. **Create Rule**

<p align="center">
  <img src="Images/Image%2025.png" img width="905" height="773" alt="image">
</p>

---

> **Note:** This lab is intentionally left open. The Okta org configured 
> here serves as the foundation for all subsequent Okta labs in the 
> [Okta IAM Lab Series](https://github.com/RyanKennon/Okta-Lab-Series/tree/main).

---

<p align="right">
  <a href="https://github.com/RyanKennon/okta-AD-integration">Lab 2 — Okta Active Directory Integration ➡</a>
</p>
