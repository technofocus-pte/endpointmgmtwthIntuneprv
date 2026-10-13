# Lab 13 – Enabling Remote Help

### Summary

In this lab, you will enable and configure **Remote Help** in Microsoft Intune. Remote Help is a cloud-based remote assistance tool that allows IT support staff to remotely view and troubleshoot Windows devices enrolled in Intune. You will activate Remote Help, configure role-based permissions, and test a Remote Help session between a helpdesk technician and a user.

### Prerequisites

Before beginning this lab, ensure the following labs are completed:

- Lab 1 – Set up Microsoft Intune
- Lab 3 – Configure Device Enrollment
- Lab 4 – Enroll Devices into Microsoft Intune
- Lab 6 – Create and Assign Configuration Profiles
- Lab 11 – Configure Endpoint Privilege Management *(recommended)*

You also need:

- **SEA-SVR1** – used by the helpdesk technician (the tenant admin account).
- **SEA-WS1** – used by the end user, **Cody Godinez**. SEA-WS1 must be enrolled in Intune and a member of the **Contoso Developer devices** group (Lab 6).

### Scenario

Contoso IT wants to provide secure remote support to its users without relying on third-party tools. Remote Help enables technicians to assist users by viewing or controlling their screen, with role-based access and session auditing. In this lab, you will enable the Remote Help feature and simulate a real remote support session.

## Exercise 1: Enable Remote Help in Intune

### Task 1: Assign Remote Help licenses

Remote Help is an Intune Suite capability. **Both** the technician (helper) and the user receiving help (sharer) need a license.

1. On **SEA-SVR1**, sign in to the **Microsoft Intune admin center** (**https://intune.microsoft.com**) as the tenant admin.

2. Select **Tenant administration** → **Intune add-ons**, and verify that **Microsoft Intune Suite** (or **Remote Help**) is listed as active.

    > **Note:** If it is not active, start the Intune Suite trial from this page before you continue.

3. Open the **Microsoft 365 admin center** (**https://admin.microsoft.com**) and select **Users** → **Active users**.

4. Select your **tenant admin** account, select **Licenses and apps**, select **Microsoft Intune Suite** (or **Remote Help**), and select **Save changes**.

5. Repeat the previous step for **Cody Godinez**.

    > **Note:** If you completed Lab 11, Cody already has the Intune Suite license.

### Task 2: Enable Remote Help settings

1. In the Intune admin center, navigate to **Tenant administration → Remote Help**.

    ![](media/media/image1.png)

2. On the **Settings** tab, click **Configure**.

    ![](media/media/image2.png)

3. In the side pane, set the following, and then click **Save**:

    - **Enable Remote Help** → *Enabled*
    - **Allow Remote Help to unenrolled devices** → *Enabled*

    ![](media/media/image3.png)

## Exercise 2: Configure RBAC Permissions for Remote Help

### Task 1: Create the Contoso Helpdesk group

Role assignments in Intune are given to **user** groups (the technicians), and are scoped to **device** groups (the devices they may help).

1. In the Intune admin center, select **Groups** → **New group**.

2. Enter the following information:

    - Group type: **Security**
    - Group name: **Contoso Helpdesk**
    - Group description: **Technicians allowed to use Remote Help**
    - Membership type: **Assigned**

3. Under **Members**, select **No members selected**, add **Miranda Snider** and your **tenant admin** account, and then choose **Select**.

4. Select **Create**.

### Task 2: Assign the Help Desk Operator role

1. In the Intune admin center, go to **Tenant administration → Roles**.

    ![](media/media/image4.png)

2. Select **Help Desk Operator**.

    ![](media/media/image5.png)

3. On the **Assignments** page, click **+ Assign**.

    ![](media/media/image6.png)

4. On the **Basics** tab, enter the name **Remote help role** and click **Next**.

    ![](media/media/image7.png)

5. On the **Admin groups** tab, click **Add groups**, select **Contoso Helpdesk**, click **Select**, and then click **Next**.

    ![](media/media/image8.png)

    ![](media/media/image9.png)

    ![](media/media/image10.png)

6. On the **Scope groups** tab, select **Add groups**, select **Contoso Developer devices**, click **Select**, and then click **Next**.

    ![](media/media/image11.png)

7. On the **Scope tags** tab, click **Next**, and then click **Create** on the **Review + create** tab to save the role assignment.

    ![](media/media/image12.png)

    ![](media/media/image13.png)

    Members of **Contoso Helpdesk** can now start Remote Help sessions with devices in **Contoso Developer devices**.

## Exercise 3: Install the Remote Help App

### Task 1: Install Remote Help on SEA-SVR1

1. On **SEA-SVR1**, open Microsoft Edge.

2. Go to **https://aka.ms/DownloadRemoteHelp** and download the Remote Help installer.

    ![](media/media/image14.png)

3. Run the installer, accept the license terms, and complete the installation.

    ![](media/media/image15.png)

    ![](media/media/image16.png)

### Task 2: Install Remote Help on SEA-WS1

Installing an app requires local administrator rights. Cody is a standard user, so you install Remote Help as **Cindy White**, who is a local administrator on SEA-WS1 because she joined it to Microsoft Entra ID in Lab 4.

1. Switch to **SEA-WS1** and sign in as **Cindy@M365xXXXXXXX.onmicrosoft.com** (substitute **XXXXXXX** with your tenant name) with the PIN **102938** or password **P@55w.rd1234**.

2. Open Edge and go to **https://aka.ms/DownloadRemoteHelp**.

    ![](media/media/image17.png)

3. Download and run the installer, accept the license terms, and complete the installation.

    ![](media/media/image18.png)

4. Sign out of SEA-WS1.

## Exercise 4: Start a Remote Support Session

### Task 1: The technician starts the session (SEA-SVR1)

1. On **SEA-SVR1**, launch **Remote Help** from the Start menu.

    > **Note:** If the app does not launch, restart SEA-SVR1 and try again.

2. Sign in with your **tenant admin** account, and click **Accept** to accept the terms and conditions.

    ![](media/media/image19.png)

3. Under **Give help**, select **Get a security code**.

    ![](media/media/image20.png)

4. A 6-digit security code is generated. Note the code — it is valid for 10 minutes.

    ![](media/media/image21.png)

### Task 2: The user joins the session (SEA-WS1)

1. Switch to **SEA-WS1** and sign in as **cgodinez@M365xXXXXXXX.onmicrosoft.com** with the password **P@55w.rd1234**.

2. Launch **Remote Help** from the Start menu. If prompted, sign in as Cody and accept the terms.

3. Under **Get help**, enter the 6-digit code from SEA-SVR1 and select **Submit**.

    ![](media/media/image22.png)

### Task 3: Establish the session

1. On **SEA-SVR1**, Remote Help shows Cody's name, device, and enrollment status. Choose one of the following:

    - **View screen**
    - **Take full control**

    ![](media/media/image23.png)

2. On **SEA-WS1**, Cody sees a prompt requesting permission. Select **Allow**.

    ![](media/media/image24.png)

3. On **SEA-SVR1**, confirm that you can see (or control) Cody's desktop.

    ![](media/media/image25.png)

    You now have a working Remote Help session.

4. On SEA-SVR1, select **Leave** to end the session.

## Exercise 5: Validate Logs and Session Details

### Task 1: Review Remote Help reports in Intune

1. In the Intune admin center, go to **Tenant administration → Remote Help**, and then select the **Remote Help sessions** tab.

    ![](media/media/image26.png)

2. Review the following details for the session you just completed:

    - Session status
    - Duration
    - Technician (helper)
    - User assisted (sharer)
    - Session type (view or full control)

    > **Note:** It can take a few minutes for a completed session to appear in the list.

### Results

After completing this lab, you will have:

- Activated the Remote Help feature in Microsoft Intune
- Configured Remote Help permissions with an RBAC role assignment
- Installed the Remote Help application on technician and user endpoints
- Performed a full Remote Help assistance session
- Reviewed the session in the Remote Help report

Contoso is now ready to provide secure, integrated remote support to end users using Microsoft Intune.
