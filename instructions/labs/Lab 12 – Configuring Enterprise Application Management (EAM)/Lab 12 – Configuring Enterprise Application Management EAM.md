# Lab 12 – Configuring Enterprise Application Management (EAM)

### Summary

In this lab, you will configure **Enterprise Application Management (EAM)** in Microsoft Intune. EAM provides a simpler way to deploy and manage Win32 applications using Microsoft's cloud-hosted **Enterprise App Catalog**. You will add an application to Intune from the catalog, assign it to devices, verify installation on a managed Windows client, and review the deployment status.

### Prerequisites

Before starting this lab, ensure the following labs are completed:

- Lab 1 – Set up Microsoft Intune
- Lab 2 – Manage Microsoft Entra Device Registration
- Lab 3 – Configure and Manage Device Enrollment
- Lab 4 – Enroll Devices into Microsoft Intune
- Lab 6 – Create and Assign Configuration Profiles
- Lab 11 – Configure Endpoint Privilege Management (EPM) *(recommended)*

You will also need:

- **SEA-WS1** enrolled in Intune and a member of the **Contoso Developer devices** group (Lab 6).
- Admin access to the Intune admin center.

### Scenario

Contoso IT wants to simplify application lifecycle management for commonly used desktop applications. Instead of manually packaging .exe files and maintaining detection rules, the team will use **Enterprise Application Management (EAM)** to deploy pre-packaged, Microsoft-maintained Win32 apps.

In this lab, you will use EAM to deploy **7-Zip** and validate the deployment on SEA-WS1.

## Exercise 1: Verify Enterprise Application Management is available

### Task 1: Confirm the Intune Suite add-on

Enterprise Application Management is an Intune Suite capability.

1. On **SEA-SVR1**, sign in to the **Microsoft Intune admin center** (**https://intune.microsoft.com**) as the tenant admin.

    ![](media/media/image1.png)

2. Select **Tenant administration** → **Intune add-ons**, and verify that **Microsoft Intune Suite** (or **Enterprise Application Management**) is listed as active.

    > **Note:** If you completed Lab 11, the Intune Suite trial is already active. If it is not active, start the Intune Suite trial from this page before you continue.

3. In the left navigation pane, select **Apps**.

    ![](media/media/image2.png)

## Exercise 2: Add an Application from the Enterprise App Catalog

### Task 1: Select and add 7-Zip

1. Select **All apps**.

    ![](media/media/image3.png)

2. On the **Apps | All apps** page, click **+ Create**.

    ![](media/media/image4.png)

3. In the **App type** dropdown, select **Enterprise App Catalog app** and click **Select**.

    ![](media/media/image5.png)

    ![](media/media/image6.png)

4. On the **App information** tab, click **Search the Enterprise App Catalog**.

5. Search for **7-Zip**, select it from the list, and click **Next**.

    ![](media/media/image7.png)

6. On the configuration page, select the **7-Zip (x64)** package and click **Select**.

7. On the **App information** tab, review the details that are filled in from the catalog and click **Next**.

    ![](media/media/image8.png)

8. On the **Program** tab, review the default install and uninstall commands and click **Next**.

    ![](media/media/image9.png)

9. On the **Requirements** tab, click **Next**.

    ![](media/media/image10.png)

10. On the **Detection rules** tab, click **Next**.

    ![](media/media/image11.png)

    > **Note:** The detection rules, install commands, and requirements are created for you from the catalog. This is the packaging work that EAM saves you.

11. On the **Supersedence** tab, click **Next**.

    ![](media/media/image12.png)

12. On the **Assignments** tab, under **Required**, select **+ Add group**, select **Contoso Developer devices**, click **Select**, and then click **Next**.

    ![](media/media/image13.png)

    > **Note:** The app must be assigned as **Required** so that it installs automatically on SEA-WS1. **Available for enrolled devices** only works for user groups and waits for the user to install the app from Company Portal.

13. On the **Review + create** tab, click **Create**.

    ![](media/media/image14.png)

    ![](media/media/image15.png)

    7-Zip is now added to Intune as a managed Enterprise App Catalog application.

## Exercise 3: Validate Application Deployment on SEA-WS1

### Task 1: Sync the device

1. Switch to **SEA-WS1** and sign in as **Cody Godinez** (**cgodinez@M365xXXXXXXX.onmicrosoft.com**, password **P@55w.rd1234**).

2. Open **Settings → Accounts → Access work or school**.

    ![](media/media/image16.png)

3. Select **Connected to Contoso's Azure AD** → **Info**, scroll down, and select **Sync**.

    ![](media/media/image17.png)

    ![](media/media/image18.png)

### Task 2: Check for the installed application

1. Wait 10–15 minutes, and then open the **Start** menu and select **All apps**.

    > **Note:** Win32 apps are installed by the Intune Management Extension, which checks in on its own schedule, so the app can take longer to arrive than a configuration profile. If 7-Zip has not appeared after 15 minutes, restart SEA-WS1, sign in again as Cody, and wait a few more minutes.

2. Scroll to find **7-Zip File Manager**.

    ![](media/media/image19.png)

3. Launch the app to confirm the installation.

    ![](media/media/image20.png)

## Exercise 4: Review Deployment Status in Intune

### Task 1: Check installation reports

1. On **SEA-SVR1**, in the Intune admin center, go to **Apps → All apps** and select **7-Zip**.

    ![](media/media/image21.png)

    ![](media/media/image22.png)

2. On the app's **Overview** page, select **Device install status** and **User install status**, and verify that **SEA-WS1** shows as **Installed**.

    ![](media/media/image23.png)

    ![](media/media/image24.png)

### Results

After completing this lab, you will have:

- Verified that Enterprise Application Management is available in the tenant
- Added a Win32 application from the Enterprise App Catalog without manual packaging
- Assigned and deployed the application to Windows devices
- Validated app installation on a managed client
- Reviewed device and user install status in Intune

Contoso now benefits from simplified Win32 app lifecycle management.
