# Lab 11 – Configure Endpoint Privilege Management (EPM) in Microsoft Intune

**Summary**

In this lab, you will configure **Endpoint Privilege Management (EPM)**
using Microsoft Intune to provide standard users with **just‑in‑time**
and **controlled elevation** for specific administrative tasks. You will
create an **EPM Elevation Settings Policy**, an **Elevation Rule
Policy**, assign these policies to Contoso devices, and verify delegated
elevation using a standard user account on SEA‑WS1.

This feature allows Contoso users to run approved apps with elevated
permissions **without providing full admin rights** or distributing
local admin credentials.

------------------------------------------------------------------------

**Prerequisites**

The following labs must be completed before this lab:

- Lab 1 – Set up Microsoft Intune

- Lab 2 – Manage Microsoft Entra Device Registration

- Lab 3 – Configure and Manage Device Enrollment

- Lab 4 – Enroll Devices into Microsoft Intune

- Lab 6 – Create and Assign Configuration Profiles

- You will also need:

&nbsp;

- A Windows 11 device (SEA‑WS1) enrolled in Intune

- A standard user account (Cindy White)

- An admin account to configure Intune policies

------------------------------------------------------------------------

## Exercise 1: Enable Endpoint Privilege Management

**Scenario**

Contoso wants to reduce the number of local administrators on Windows
devices. Developers need temporary elevation to run specific tools, but
granting full admin rights introduces risk. You will enable EPM to give
**controlled elevation** only for approved applications.

### Task 1: Create the Elevation Settings Policy

1.  In the Intune admin center, select **Endpoint security,** select
    **Endpoint Privilege Management**.

> ![](media/media/image1.png)

2.  Click **+ Create Policy** → choose the following and click
    **Create.**

> Platform: Windows
>
> Profile: Elevation settings policy
>
> ![](media/media/image2.png)

3.  Configure the following on the **Basics** tab and click **Next.**

- Name: **Contoso – EPM Elevation Settings**

- Description: **Configures global elevation behavior for Contoso
  devices**

> ![](media/media/image3.png)

4.  On the **Configuration Settings** tab **expand Privilege management
    elevation client settings** page, enable EPM, default elevation
    response to **Require support approval** and click **Next.**

![](media/media/image4.png)

5.  On the scope tags tab click **Next.**

6.  On the **Assignments** page assign to: **Contoso Developer devices**

![](media/media/image5.png)

7.  Click **Next** → **Create**.

![](media/media/image6.png)

------------------------------------------------------------------------

## Exercise 2: Create an Elevation Rule Policy

**Scenario**

Developers at Contoso need administrative rights to install or run
**DevBuildTool.exe**, a trusted internal app. Instead of giving them
admin accounts, you'll configure EPM to allow elevation *only* for this
application.

------------------------------------------------------------------------

**Task 1: Create the Application Elevation Rule**

1.  Go to **Endpoint security** → **Endpoint Privilege Management**.

2.  Select **+ Create Policy** → **Elevation rules policy** and click
    **Create.**

> ![](media/media/image7.png)

3.  On the **Basics** tab enter the following and click Next

- Name: **Contoso – EPM Elevation Rule: DevBuildTool**

- Description: **Allows elevation for DevBuildTool.exe for developer
  devices**

> ![](media/media/image8.png)

4.  On the **Rules** tab click **+ Add** to create a new rule:

- **Rule Name:** Adobe rule

- **Elevation type:** Choose support approved

> ![](media/media/image9.png)

- **File name:** Enter the exe file name that is downloaded in the ,
  here we use adobe_en_install.exe

- **File path:** Enter the exe file path from the VM

> **Note:** For File hash run the following command in the terminal of
> the virtual machine.  
> Get-FileHash (path of the exe file in the device location)
>
> ![](media/media/image10.png)
>
> ![](media/media/image11.png)

5.  Click **Save**, then **Next**.

> ![](media/media/image12.png)

6.  On the **Assignments** tab select All users, all devices.

![](media/media/image13.png)

7.  Click **Next** → **Create**.

![](media/media/image14.png)

![](media/media/image15.png)

------------------------------------------------------------------------

## Exercise 3: Sync Device to Apply EPM Policies

**Task 1: Sync SEA‑WS1**

1.  On **SEA‑WS1**, sign in as **Cody Godinez.**.

2.  Open **Settings → Accounts → Access work or school**.

> ![](media/media/image16.png)

3.  Select **Connected to Contoso** → **Info**.

> ![](media/media/image17.png)

4.  Scroll down and select **Sync**.

> ![](media/media/image18.png)

5.  Wait a few minutes for policy refresh.

------------------------------------------------------------------------

## Exercise 4: Test EPM Elevation on SEA‑WS1

**Scenario**

Cgodinez needs elevated privileges to run DevBuildTool.exe but does not
have admin rights.

------------------------------------------------------------------------

**Task 1: Attempt to Run the Application**

1.  On SEA‑WS1, locate **adobe.exe**.

> ![](media/media/image19.png)

2.  Right-click the app.

    - Because EPM is enabled, Cody should see an **Elevation prompt
      (EPM)**

> ![](media/media/image20.png)

3.  Provide a **justification** and click **Continue**. If prompted
    enter the credentials and Send.

> ![](media/media/image21.png)
>
> ![](media/media/image22.png)

------------------------------------------------------------------------

## Exercise 5: Verify EPM Reporting

**Task 1: View Elevation Reports**

1.  In the Intune admin center, navigate to:  
    **Reports → Endpoint Privilege Management**

> ![](media/media/image23.png)
>
> ![](media/media/image24.png)

2.  Review:

    - Recent elevation attempts

    - App-based elevation rules

    - Justifications submitted by Cindy

    - Approval outcomes

------------------------------------------------------------------------

**Results**

After completing this lab, you will have:

- Enabled **Endpoint Privilege Management** in Intune

- Created an **Elevation Settings Policy**

- Configured an **Elevation Rule Policy** for a specific application

- Assigned EPM rules to Windows 11 devices

- Tested delegated elevation on SEA‑WS1

- Verified event logs and reporting for elevation attempts

EPM is now fully deployed in Contoso, allowing secure, controlled admin
privilege elevation without granting full administrator accounts.
