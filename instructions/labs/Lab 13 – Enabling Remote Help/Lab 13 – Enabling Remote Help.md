# Lab 13 – Enabling Remote Help

**Summary**

In this lab, you will enable and configure **Remote Help** in Microsoft
Intune. Remote Help is a cloud-based remote assistance tool that allows
IT support staff to remotely view and troubleshoot Windows devices
enrolled in Intune. You will activate the Remote Help add‑on, configure
permissions, and test a Remote Help session between the helpdesk
technician and the user.

------------------------------------------------------------------------

**Prerequisites**

Before beginning this lab, ensure the following labs are completed:

- Lab 1 – Set up Microsoft Intune

- Lab 3 – Configure Device Enrollment

- Lab 4 – Enroll Devices into Microsoft Intune

- Lab 12 – Configuring Enterprise Application Management *(optional)*

You also need:

- **Microsoft Intune Suite** or **Remote Help add‑on** trial activated

- Two Windows 10/11 devices:

  - SEA‑SVR1 (admin / helpdesk technician)

  - SEA‑WS1 (end user – Cindy White)

------------------------------------------------------------------------

**Scenario**

Contoso IT wants to provide secure remote support to its users without
relying on third‑party tools. Remote Help enables technicians to assist
users by viewing or controlling their screen, with role‑based access and
session auditing. In this lab, you will enable the Remote Help feature
and simulate a real remote support session.

------------------------------------------------------------------------

## Exercise 1: Enable Remote Help in Intune

------------------------------------------------------------------------

### Task 1: Enable Remote Help Settings

1.  In the Intune admin center, navigate to:  
    **Tenant administration → Remote Help**

> ![](media/media/image1.png)

2.  Under Settings tab, click **Configure**.

> ![](media/media/image2.png)

3.  On the side pane, **enable** remote help, **allow** remote help to
    unenroll devices and click **Save.**

> ![](media/media/image3.png)

------------------------------------------------------------------------

## Exercise 2: Configure RBAC Permissions for Remote Help

### Task 1: Assign Help Desk Role

1.  In the Intune admin center, go to **Tenant administration → Roles**.

> ![](media/media/image4.png)

2.  Select **Help Desk Operator**.

> ![](media/media/image5.png)

3.  On the **Assignments** tab, click **+Assign.**

> ![](media/media/image6.png)

4.  On the Basics tab, enter the name as **Remote help role**

> ![](media/media/image7.png)

5.  On **Admin groups** click **Add groups** and select Contoso
    Developers device![](media/media/image8.png)

> ![](media/media/image9.png)
>
> ![](media/media/image10.png)

6.  Assign the role to the technician account:

    - User: **All User**

    - Scope: **All devices**

> ![](media/media/image11.png)

7.  Click **Next** on Scope tags and then click **Create** on the
    Review + Create tab to save the role assignment.

> ![](media/media/image12.png)
>
> ![](media/media/image13.png)

This ensures your helpdesk user can start Remote Help sessions.

------------------------------------------------------------------------

## Exercise 3: Install Remote Help App

### Task 1: Install Remote Help on SEA‑SVR1

1.  On **SEA‑SVR1**, open Microsoft Edge.

2.  Visit:  
    **https://aka.ms/DownloadRemoteHelp**

3.  Download the Remote Help installer.

> ![](media/media/image14.png)

4.  Run the installer and complete installation.

> ![](media/media/image15.png)
>
> ![](media/media/image16.png)

### Task 2: Install Remote Help on SEA‑WS1 (End User)

1.  Sign in as **Cody Godinez** on SEA‑WS1.

2.  Open Edge and go to:  
    [**https://aka.ms/DownloadRemoteHelp**](https://aka.ms/DownloadRemoteHelp)

> ![](media/media/image17.png)

3.  Download and install Remote Help.

> ![](media/media/image18.png)

------------------------------------------------------------------------

**Exercise 4: Start a Remote Support Session**

**Task 1: Technician Initiates the Session (SEA‑SVR1)**

1.  Launch **Remote Help**.

> Note: if the app does not launch, then restart the PC.

2.  Sign in with your **admin** account, and click Accept to accept the
    terms and conditions.

> ![](media/media/image19.png)

3.  Select **Give help**.

> ![](media/media/image20.png)

4.  A 6‑digit security code is generated. Copy the security code.

> ![](media/media/image21.png)

------------------------------------------------------------------------

**Task 2: End User Joins the Session (SEA‑WS1)**

1.  Launch **Remote Help**.

2.  Sign in as **Cody godinez**.

3.  Select **Get help**.

4.  Enter the 6‑digit code shared by the administrator.

> ![](media/media/image22.png)

5.  Click **Start session**.

Cindy will see a prompt requesting permission.

------------------------------------------------------------------------

**Task 3: Establishing the Session**

1.  On SEA‑WS1, click **Allow** to grant screen‑sharing permission.

2.  On SEA‑SVR1, choose:

    - **View screen**  
      or

    - **Take full control**

> ![](media/media/image23.png)
>
> ![](media/media/image24.png)
>
> ![](media/media/image25.png)

You now have a working Remote Help session.

------------------------------------------------------------------------

## Exercise 5: Validate Logs and Session Details

### Task 1: Review Remote Help Reports in Intune

1.  In the Intune admin center, go to:  
    **Tenant administration → Remote Help 🡪 Remote Help sessions**

> ![](media/media/image26.png)

2.  Review:

    - Successful sessions

    - Duration

    - Technician

    - User assisted

    - Session type (view or control)

------------------------------------------------------------------------

**Results**

After completing this lab, you will have:

- Activated the Remote Help feature in Microsoft Intune

- Configured Remote Help permissions and capabilities

- Installed the Remote Help application on technician and user endpoints

- Performed a full Remote Help assistance session

Contoso is now ready to provide secure, integrated remote support to end
users using Microsoft Intune
