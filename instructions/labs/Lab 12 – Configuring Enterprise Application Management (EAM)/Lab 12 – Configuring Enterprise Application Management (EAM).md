# Lab 12 – Configuring Enterprise Application Management (EAM)

**Summary**

In this lab, you will configure **Enterprise Application Management
(EAM)** in Microsoft Intune. EAM provides an automated way to deploy,
update, and manage Win32 applications using Microsoft’s cloud‑hosted app
catalog. You will explore the Enterprise App Catalog, add an application
to Intune using EAM, configure automatic updates, assign the application
to devices, and verify installation on a managed Windows client.

------------------------------------------------------------------------

**Prerequisites**

Before starting this lab, ensure the following labs are completed:

- Lab 1 – Set up Microsoft Intune

- Lab 2 – Manage Microsoft Entra Device Registration

- Lab 3 – Configure and Manage Device Enrollment

- Lab 4 – Enroll Devices into Microsoft Intune

- Lab 11 – Configure Endpoint Privilege Management (EPM) *(optional but
  recommended)*

Other Requirements:

- **Microsoft Intune Suite** enabled for the tenant

- A Windows 11 device enrolled in Intune (SEA‑WS1 or SEA‑WS2)

- Admin access to the Intune admin center

------------------------------------------------------------------------

**Scenario**

Contoso IT wants to simplify application lifecycle management for
commonly used desktop applications. Instead of manually packaging .exe
files and maintaining detection rules, the team will leverage
**Enterprise Application Management (EAM)** to deploy pre-packaged,
Microsoft‑maintained Win32 apps.

In this lab, you will use EAM to automatically deploy **7‑Zip**,
configure ongoing updates, and validate the deployment on SEA‑WS1.

------------------------------------------------------------------------

## Exercise 1: Explore the Enterprise Application Management Catalog

### Task 1: Locate the EAM Portal

1.  Sign in to the **Microsoft Intune admin center**.

> ![](media/media/image1.png)

2.  In the left navigation pane, select **Apps**.

3.  Under Apps, ensure the tab for **Enterprise app catalog** is
    present.

> ![](media/media/image2.png)

------------------------------------------------------------------------

## Exercise 2: Add an Application from the EAM Catalog

### Task 1: Select and Add an Application

1.  Click All Apps.

> ![](media/media/image3.png)

2.  On the **Apps| All Apps** page click **Create.**

> ![](media/media/image4.png)

3.  On the App type dropdown select **Enterprise App catalog app** and
    click on the **Select** button.

> ![](media/media/image5.png)
>
> ![](media/media/image6.png)

4.  Under **Select App** blade, click on **Search the Enterprise App
    Catalog**.

5.  Select **7‑Zip** from the list and click **Next.**

> ![](media/media/image7.png)

6.  On the Configuration tab click on the app and click **Select**.

7.  On the App information tab click Next.

![](media/media/image8.png)

8.  On the Program tab review the default options and click **Next.**

![](media/media/image9.png)

9.  On the Requirements tab, click **Next.**

> ![](media/media/image10.png)

10. On the detection rules tab, click **Next**.

> ![](media/media/image11.png)

11. On the Supersedence tab, click **Next.**

> ![](media/media/image12.png)

12. On the Assignments tab, select **Contoso Developer** **devices**
    group and click **Next**.

> ![](media/media/image13.png)

13. Click **Add app** on the **Review+ create** tab.

> ![](media/media/image14.png)
>
> ![](media/media/image15.png)

7‑Zip is now added to Intune as a managed EAM application.

------------------------------------------------------------------------

## Exercise 3: Validate Application Deployment on SEA‑WS1

### Task 1: Sync Policies

1.  On **SEA‑WS1**, sign in as **Cody Godinez**.

2.  Open **Settings → Accounts → Access work or school**.

> ![](media/media/image16.png)

3.  Select **Info** and click **Sync**.

> ![](media/media/image17.png)
>
> ![](media/media/image18.png)

------------------------------------------------------------------------

### Task 2: Check for Installed Application

1.  After 2–5 minutes, open the Start Menu.

2.  Scroll to find **7‑Zip File Manager**.

> ![](media/media/image19.png)

3.  Launch the app to confirm installation.

> ![](media/media/image20.png)

If the app does not appear immediately, wait 5–10 minutes or reboot the
device.

------------------------------------------------------------------------

## Exercise 4: Review Deployment Status in Intune

### Task 1: Check Installation Reports

1.  In the Intune admin center, go to **Apps → All apps**, select
    **Contoso – 7‑Zip**.

> ![](media/media/image21.png)
>
> ![](media/media/image22.png)

2.  Review:

    - Device install status

    - User install status

![](media/media/image23.png)

![](media/media/image24.png)

------------------------------------------------------------------------

------------------------------------------------------------------------

**Results**

After completing this lab, you will have:

- Explored the Enterprise Application Management (EAM) interface

- Added a Win32 application from the EAM App Catalog

- Configured automatic application updates

- Assigned and deployed an application to Windows devices

- Validated app installation on a managed client

Contoso now benefits from automated and simplified Win32 app lifecycle
management.
