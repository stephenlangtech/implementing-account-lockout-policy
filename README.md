# Configuring Account Lockout Policy Using Group Policy in Active Directory

In this tutorial, we configure an Account Lockout Policy using Group Policy in an Active Directory environment. The policy is configured to lock a domain user account after multiple unsuccessful login attempts and automatically unlock the account after a specified period. This lab uses VMware Workstation with one Domain Controller and two Windows client virtual machines to demonstrate how Group Policy can centrally enforce account security policies across domain-joined computers.

## Environments and Technologies Used

* VMware Workstation
* Windows Server
* Active Directory Domain Services (AD DS)
* Group Policy Management
* Group Policy Objects (GPOs)
* Windows Command Line

## Operating Systems Used

* Windows Server
* Windows 10

## Actions and Observations

### 1. Open Group Policy Management

* Open **Group Policy Management** on the Domain Controller.
* Expand the domain.
* Right-click **Default Domain Policy**.
* Select:
  **Edit**

  <img src="Screenshot 2026-09-27 101624.png" width="50%" height="50%">  

  <img src="Screenshot 2026-09-27 101635.png" width="50%" height="50%">  

### 2. Configure the Account Lockout Threshold

* Navigate to:

  **Computer Configuration**
  → **Policies**
  → **Windows Settings**
  → **Security Settings**
  → **Account Policies**
  → **Account Lockout Policy**

* Locate:
  **Account lockout threshold**

* Right-click the policy and select:
  **Properties**

* Set the value to:
  **5 invalid login attempts**

* Click:
  **Apply**

* Click:
  **OK**

This setting determines how many unsuccessful login attempts are allowed before an Active Directory user account becomes locked.  

  <img src="Screenshot 2026-09-27 101755.png" width="65%" height="65%">  

### 3. Configure the Account Lockout Duration

* Locate:
  **Account lockout duration**
* Right-click the policy and select:
  **Properties**
* Set the duration to:
  **30 minutes**
* Windows will automatically recommend setting **Reset account lockout counter after** to the same duration.
* Accept the recommended **30-minute** value.
* Click:
  **Apply**
* Click:
  **OK**

The account will remain locked for 30 minutes before it can automatically become available again, assuming no other administrative action is taken.  

  <img src="Screenshot 2026-09-27 101801.png" width="80%" height="80%">  

### 4. Force a Group Policy Update

* Group Policy may take some time to automatically apply.
* To immediately request a Group Policy refresh, open **Command Prompt** on the client VM and run:

```cmd
gpupdate /force
```

* This forces the client to retrieve and process the latest applicable Group Policy settings.

  <img src="Screenshot 2026-09-27 101210.png" width="65%" height="65%">  

### 5. Verify the Account Lockout Policy

* Log in to one of the domain-joined client VMs using a domain user account.
* Enter an incorrect password multiple times.
* After **5 unsuccessful login attempts**, the account should become locked according to the configured policy.
* The account lockout can be verified by attempting to log in again or by checking the user's account status in **Active Directory Users and Computers**.

The policy can also be tested on multiple domain-joined client VMs to verify that the Account Lockout Policy is being centrally enforced throughout the domain.

## Results

The **Account Lockout Policy** was successfully configured through Group Policy to lock user accounts after **5 unsuccessful login attempts** and maintain the lockout for **30 minutes**. The lockout counter was also configured to reset after 30 minutes.

This demonstrates how Active Directory and Group Policy can be used to centrally enforce account security policies across a domain, helping protect user accounts against repeated unauthorized login attempts.
