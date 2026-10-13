# Lab 11 – Configure Endpoint Privilege Management (EPM) in Microsoft Intune

### Summary

In this lab, you will configure **Endpoint Privilege Management (EPM)** using Microsoft Intune to provide standard users with **just-in-time** and **controlled elevation** for specific administrative tasks. You will create an **EPM Elevation Settings Policy** and an **Elevation Rule Policy**, assign these policies to Contoso devices, and verify support-approved elevation using a standard user account on SEA-WS1.

This feature allows Contoso users to run approved apps with elevated permissions **without providing full admin rights** or distributing local admin credentials.

### Prerequisites

The following labs must be completed before this lab:

- Lab 1 – Set up Microsoft Intune
- Lab 2 – Manage Microsoft Entra Device Registration
- Lab 3 – Configure and Manage Device Enrollment
- Lab 4 – Enroll Devices into Microsoft Intune
- Lab 6 – Create and Assign Configuration Profiles

You will also need:

- **SEA-WS1** enrolled in Intune and a member of the **Contoso Developer devices** group (Lab 6).
- **Cody Godinez** as the standard (non-admin) test user. Cody was created and licensed in Lab 1.
- The tenant admin account to configure Intune policies.

> **Note:** This lab uses **Cody Godinez** rather than Cindy White. Cindy joined SEA-WS1 to Microsoft Entra ID in Lab 4, and the user who joins a device becomes a local administrator on it, so she would never see an elevation prompt.

## Exercise 1: Enable Endpoint Privilege Management

### Scenario

Contoso wants to reduce the number of local administrators on Windows devices. Developers need temporary elevation to run specific installers and tools, but granting full admin rights introduces risk. You will enable EPM to give **controlled elevation** only for approved applications.

### Task 1: Verify the Intune Suite license

Endpoint Privilege Management is an Intune Suite capability and is licensed per user.

1. On **SEA-SVR1**, in the **Microsoft Intune admin center** (**https://intune.microsoft.com**), select **Tenant administration** → **Intune add-ons**. Verify that **Microsoft Intune Suite** (or **Endpoint Privilege Management**) is listed as active.

    > **Note:** If it is not active, start the Intune Suite trial from this page before you continue.

2. Open the **Microsoft 365 admin center** (**https://admin.microsoft.com**) and select **Users** → **Active users** → **Cody Godinez** → **Licenses and apps**.

3. Select **Microsoft Intune Suite** (or **Microsoft Intune Endpoint Privilege Management**) and select **Save changes**.

### Task 2: Create the Elevation Settings Policy

1. In the Intune admin center, select **Endpoint security**, then select **Endpoint Privilege Management**.

    ![](media/media/image1.png)

2. Click **+ Create Policy**, choose the following, and click **Create**:

    - Platform: **Windows**
    - Profile: **Elevation settings policy**

    ![](media/media/image2.png)

3. On the **Basics** tab, enter the following and click **Next**:

    - Name: **Contoso – EPM Elevation Settings**
    - Description: **Configures global elevation behavior for Contoso devices**

    ![](media/media/image3.png)

4. On the **Configuration settings** tab, expand **Privilege management elevation client settings** and configure the following, and then click **Next**:

    - **Endpoint Privilege Management** → *Enabled*
    - **Default elevation response** → *Require support approval*
    - **Send elevation data for reporting** → *Yes*
    - **Reporting scope** → *Diagnostic data and all endpoint elevations*

    ![](media/media/image4.png)

5. On the **Scope tags** tab, click **Next**.

6. On the **Assignments** tab, under **Included groups**, select **Add groups**, select **Contoso Developer devices**, and click **Select**.

    ![](media/media/image5.png)

7. Click **Next** → **Create**.

    ![](media/media/image6.png)

## Exercise 2: Create an Elevation Rule Policy

### Scenario

Developers at Contoso need administrative rights to run the **Adobe Acrobat Reader installer**. Instead of giving them admin accounts, you'll configure EPM to allow elevation for *only* this file, after approval by the support team.

An elevation rule identifies the file by its name, path, and **file hash**, so you first place the installer on SEA-WS1 and read its hash there.

### Task 1: Prepare the installer on SEA-WS1

1. Switch to **SEA-WS1** and sign in as **cgodinez@M365xXXXXXXX.onmicrosoft.com** (substitute **XXXXXXX** with your tenant name) with the password **P@55w.rd1234**. If prompted to set up Windows Hello, create the PIN **102938**.

2. Open **Microsoft Edge**, go to **https://get.adobe.com/reader/**, and download the **Adobe Acrobat Reader** installer.

3. Open **File Explorer**, create the folder **C:\EPM**, and move the downloaded installer from **Downloads** into **C:\EPM**.

    > **Note:** Take note of the exact file name of the installer (for example, **Reader_en_install.exe**). You will use this name in the rule.

    ![](media/media/image19.png)

4. Right-click **Start**, select **Terminal**, and run the following command to copy the installer's SHA256 hash to the clipboard. Replace **Reader_en_install.exe** with your file name if it is different.

    ```powershell
    (Get-FileHash -Path "C:\EPM\Reader_en_install.exe" -Algorithm SHA256).Hash | Set-Clipboard
    ```

    ![](media/media/image10.png)

5. Keep the Terminal window open. You will paste the hash in the next task.

### Task 2: Create the application elevation rule

To paste the hash without copying it between VMs, you create the rule from an InPrivate browser window on SEA-WS1.

1. On **SEA-WS1**, open **Microsoft Edge**, press **Ctrl+Shift+N** to open an **InPrivate** window, go to **https://intune.microsoft.com**, and sign in with the tenant admin account.

2. Go to **Endpoint security** → **Endpoint Privilege Management**.

3. Select **+ Create Policy**. Choose Platform **Windows** and Profile **Elevation rules policy**, and click **Create**.

    ![](media/media/image7.png)

4. On the **Basics** tab, enter the following and click **Next**:

    - Name: **Contoso – EPM Elevation Rule: Acrobat Reader**
    - Description: **Allows support-approved elevation for the Acrobat Reader installer**

    ![](media/media/image8.png)

5. On the **Configuration settings** tab, click **+ Add** to create a new rule and enter the following:

    - **Rule name:** **Acrobat Reader installer**
    - **Elevation type:** **Support approved**
    - **File name:** the exact installer file name, for example **Reader_en_install.exe**
    - **File path:** **C:\EPM**
    - **File hash:** press **Ctrl+V** to paste the hash you copied in Task 1

    ![](media/media/image9.png)

    ![](media/media/image11.png)

6. Click **Save**, then **Next**.

    ![](media/media/image12.png)

7. On the **Scope tags** tab, click **Next**.

8. On the **Assignments** tab, under **Included groups**, select **Add groups**, select **Contoso Developer devices**, and click **Select**.

    ![](media/media/image13.png)

9. Click **Next** → **Create**.

    ![](media/media/image14.png)

    ![](media/media/image15.png)

10. Close the InPrivate window.

## Exercise 3: Sync Device to Apply EPM Policies

### Task 1: Sync SEA-WS1

1. On **SEA-WS1**, still signed in as **Cody Godinez**, open **Settings → Accounts → Access work or school**.

    ![](media/media/image16.png)

2. Select **Connected to Contoso's Azure AD** → **Info**.

    ![](media/media/image17.png)

3. Scroll down and select **Sync**.

    ![](media/media/image18.png)

4. Wait about 10 minutes for the EPM client to install and the policies to apply.

    > **Tip:** When EPM is ready, right-clicking an .exe file shows the **Run with elevated access** option. If you don't see it yet, sync again and wait a few more minutes.

## Exercise 4: Request Elevation on SEA-WS1

### Scenario

Cody needs to run the Acrobat Reader installer but does not have admin rights.

### Task 1: Submit an elevation request

1. On **SEA-WS1**, in **File Explorer**, open **C:\EPM**.

2. Double-click the installer.

    Notice that Windows asks for administrator credentials. Cody is a standard user, so he can't install the app on his own. Select **No** to close the prompt.

3. Right-click the installer and select **Run with elevated access**.

    ![](media/media/image20.png)

4. Because the rule requires support approval, EPM asks for a reason. Enter the justification **Need Acrobat Reader to review project PDFs** and select **Submit for approval**.

    ![](media/media/image21.png)

    ![](media/media/image22.png)

## Exercise 5: Approve the elevation request

### Task 1: Approve the request in Intune

1. Switch to **SEA-SVR1**. In the **Microsoft Intune admin center**, go to **Endpoint security** → **Endpoint Privilege Management**.

2. Select the **Elevation requests** tab. Select the pending request from **Cody Godinez** for the Acrobat Reader installer.

3. Review the file details and the justification, select **Approve**, enter the reason **Approved for project work**, and confirm.

### Task 2: Run the approved app

1. Switch to **SEA-WS1**. In **C:\EPM**, right-click the installer and select **Run with elevated access** again.

    The installer now starts with administrative rights, without an admin password. Complete or cancel the installation.

    > **Note:** The approval may take a few minutes to reach the device. If the request is still pending, wait and try again. An approval is valid for a limited time (24 hours by default).

2. Sign out of **SEA-WS1**.

## Exercise 6: Verify EPM Reporting

### Task 1: View elevation reports

1. On **SEA-SVR1**, in the **Microsoft Intune admin center**, go to **Endpoint security** → **Endpoint Privilege Management** and select the **Reports** tab.

    ![](media/media/image23.png)

    ![](media/media/image24.png)

2. Open the **Elevation report** and review:

    - The elevation attempts by **Cody Godinez**
    - The rule that was applied (**Acrobat Reader installer**)
    - The justification submitted
    - The elevation type (**Support approved**)

    > **Note:** Elevation data can take up to 24 hours to appear in the reports. If the report is empty, review the request on the **Elevation requests** tab instead, where its status is now **Approved**.

### Results

After completing this lab, you will have:

- Enabled **Endpoint Privilege Management** in Intune
- Created an **Elevation Settings Policy**
- Configured an **Elevation Rule Policy** for a specific application
- Assigned EPM policies to Windows 11 devices
- Submitted, approved, and used a support-approved elevation on SEA-WS1
- Reviewed elevation requests and reports

EPM is now deployed at Contoso, allowing secure, controlled admin privilege elevation without granting full administrator accounts.
