# Lab 19 – Configure VPN Policies for Android Devices

### Summary

In this lab, you will configure **Microsoft Tunnel** and a **VPN policy for Android devices** using Microsoft Intune. You will create a Microsoft Tunnel server configuration and site, create a VPN configuration profile that uses them, assign the profile to a user group, and review its deployment status. This lab helps Contoso IT administrators prepare secure connectivity for mobile users to corporate resources.

### Prerequisites

The following lab(s) must be completed before this lab:

- Lab #1-Set up Microsoft Intune
- Lab #10-Enable Mobile Application Management (MAM) *(recommended — creates the **Contoso MAM Users** group)*

> **Note:** This lab configures Microsoft Tunnel and the Android VPN profile in Intune. A working VPN connection also needs a Linux server running the Microsoft Tunnel Gateway software and an Android device enrolled in Intune with Android Enterprise, neither of which is part of this lab environment. You will therefore create and assign the configuration, and review where its deployment status is reported, without connecting a device.

### Scenario

Contoso employees use Android devices to access internal corporate resources while working remotely. To ensure secure connectivity, Contoso wants to push VPN settings automatically to all user devices. Instead of manually configuring VPN profiles on each device, Contoso IT will deploy Intune VPN configuration profiles for centralized control.

You have been assigned to create and deploy a VPN policy for Contoso's Android users.

## Exercise 1: Create a VPN Configuration Profile for Android

### Task 1: Configure the Microsoft Tunnel Gateway

1. On **SEA-SVR1**, sign in to the **Microsoft Intune admin center** (**https://intune.microsoft.com**) as the tenant admin.

    ![](media/media/image1.png)

2. In the left navigation pane, select **Tenant administration**.

    ![](media/media/image2.png)

3. Select **Microsoft Tunnel Gateway**.

    ![](media/media/image3.png)

4. On the **Tenant admin | Microsoft Tunnel Gateway** page, select the **Server configurations** tab and click **+ Create new**.

    ![](media/media/image4.png)

5. Enter the following details and click **Next**:

    - Name: **Contoso VPN Server**
    - Description: **This server acts as the gateway endpoint for Microsoft Tunnel, allowing Android devices to establish encrypted connections to the corporate network**

    ![](media/media/image5.png)

6. On the **Settings** tab, leave the IP address range at the default, enter the following details, and click **Next**:

    - Server port: **443**
    - DNS servers: **8.8.8.8**

    ![](media/media/image6.png)

7. On the **Scope tags** tab, click **Next**.

    ![](media/media/image7.png)

8. On the **Review + create** tab, click **Create**.

    ![](media/media/image8.png)

9. Once the server configuration is created, create a site. Select the **Sites** tab.

    ![](media/media/image9.png)

10. On the **Sites** page, click **+ Create**.

    ![](media/media/image10.png)

11. Enter the following details and click **Next**:

    - Name: **Contoso secure access site**

    ![](media/media/image11.png)

12. On the **Settings** tab, enter the following details and click **Next**:

    - Public IP address or FQDN: **vpn.contoso.com**
    - Server configuration: **Contoso VPN Server**

    ![](media/media/image12.png)

    > **Note:** In production, this is the public address that Android devices use to reach your Tunnel Gateway server. **vpn.contoso.com** is a placeholder for this lab.

13. On the **Scope tags** tab, click **Next**, and then on the **Review + create** tab, click **Create**.

    ![](media/media/image13.png)

    ![](media/media/image14.png)

### Task 2: Create a new VPN profile

1. In the left navigation pane, select **Devices**.

    ![](media/media/image15.png)

2. Under **By platform**, choose **Android**.

    ![](media/media/image16.png)

3. Select **Configuration profiles**.

    ![](media/media/image17.png)

4. Click **+ Create profile**.

    ![](media/media/image18.png)

5. Set the platform to **Android Enterprise**, choose **Templates** as the profile type, select **VPN** as the template, and then click **Create**.

    ![](media/media/image19.png)

    > **Note:** Choose the **VPN** template listed under **Fully Managed, Dedicated, and Corporate-Owned Work Profile** or **Personally-Owned Work Profile**, to match how your Android devices are enrolled.

6. On the **Basics** tab, enter the following details and click **Next**:

    - Name: **Contoso – Android VPN Policy**
    - Description: **Deploys VPN settings to Contoso Android users.**

    ![](media/media/image20.png)

7. On the **Configuration settings** tab, choose the following options and click **Next**:

    - Connection type: **Microsoft Tunnel**
    - Connection name: **Contoso VPN**
    - Microsoft Tunnel site: **Contoso secure access site**

    ![](media/media/image21.png)

    > **Note:** On Android, the **Microsoft Defender for Endpoint** app acts as the Microsoft Tunnel client. In production, you also deploy that app to the same users.

8. On the **Assignments** tab, under **Included groups**, select **+ Add groups**, select **Contoso MAM Users**, choose **Select**, and then click **Next**.

    ![](media/media/image22.png)

    > **Note:** If you did not complete Lab 10, create a **Security** group named **Contoso MAM Users** with **Assigned** membership and add **Cindy White** to it (**Groups → New group**). Assigning to a specific group rather than **All users** keeps the pilot limited to the users you choose.

9. On the **Review + create** tab, check all the details and click **Create**.

    ![](media/media/image23.png)

    ![](media/media/image24.png)

### Task 3: Review the VPN profile deployment status

1. In the **Microsoft Intune admin center**, go to **Devices → Android → Configuration profiles** and select **Contoso – Android VPN Policy**.

2. On the profile **Overview** page, review the **Device and user check-in status** chart and the **Device status** and **User status** reports.

    > **Note:** Because no Android Enterprise devices are enrolled in this lab environment, the counts show **0**. When an enrolled Android device for a member of **Contoso MAM Users** checks in, it appears here as **Succeeded**, **Error**, or **Conflict**.

3. Go to **Tenant administration → Microsoft Tunnel Gateway** and select the **Health status** tab.

    > **Note:** No servers are listed because no Linux server has been installed with the Tunnel Gateway software. In production, each server you install appears here with its health checks.

**Results**

After completing this lab, you will have:

- Created a Microsoft Tunnel server configuration and site
- Created a VPN configuration profile for Android Enterprise devices
- Assigned the VPN policy to a user group
- Reviewed where VPN profile deployment and Tunnel server health are monitored

Contoso is now ready to deliver VPN settings automatically to Android users as soon as a Tunnel Gateway server is installed and devices are enrolled.
