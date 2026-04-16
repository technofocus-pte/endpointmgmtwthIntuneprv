# Lab 19 – Configure VPN Policies for Android Devices

**Summary**

In this lab, you will configure and deploy **VPN policies for Android
devices** using Microsoft Intune. You will create a VPN configuration
profile, assign it to a device/user group, and validate the VPN settings
on an enrolled Android device. This lab helps Contoso IT administrators
securely connect mobile users to corporate resources.

------------------------------------------------------------------------

**Scenario**

Contoso employees use Android devices to access internal corporate
resources while working remotely. To ensure secure connectivity, Contoso
wants to push VPN settings automatically to all user devices. Instead of
manually configuring VPN profiles on each device, Contoso IT will deploy
Intune VPN configuration profiles for centralized control.

You have been assigned to create and deploy a VPN policy for Contoso’s
Android users.

------------------------------------------------------------------------

## Exercise 1: Create a VPN Configuration Profile for Android

### Task 1: Configure Microsoft Tunnel gateway

1.  Sign in to the **Microsoft Intune admin center**.

> ![](media/media/image1.png)

2.  On the left side navigation pane, choose Tenant administrator

![](media/media/image2.png)

3.  Choose **Microsoft Tunnel Gateway.**

![](media/media/image3.png)

4.  On the **Tenant admin | Microsoft Tunnel** Gateway page, select
    **Server configurations and click** + Create new  
    ![](media/media/image4.png)

5.  Enter the following details and click **Next  
    Name:** Contoso VPN Server

**Description:** This server acts as the gateway endpoint for Microsoft
Tunnel, allowing Android and Windows devices to establish encrypted
connections to the corporate network

![](media/media/image5.png)

6.  On the settings tab, leave the IP address to default, enter the
    following details and click **Next.**

Server port: **443**

DNS Server Address: **8.8.8.8**

![](media/media/image6.png)

7.  On the Scope tags, Click **Next.**

![](media/media/image7.png)

8.  On the **Review + create** tab, click **Create.**  
    ![](media/media/image8.png)

9.  Once the Server is created, we will now create site. Go to sites
    tab.

![](media/media/image9.png)

10. On the sites page, click **Create**.

![](media/media/image10.png)

11. Enter the following details and click **Next.**

> Name: **Contoso secure access site**
>
> ![](media/media/image11.png)

12. On the settings page enter the following details and click **Next.**

Public IP address: **vpn.contoso.com**

Server Configuration: **Contoso VPN Server**

**  
**![](media/media/image12.png)

13. For scopes click **Next** on the Review + Create page click
    **Create.**

![](media/media/image13.png)

![](media/media/image14.png)

### Task 2: Create a New VPN Profile

1.  In the left navigation pane, select **Devices**.

> ![](media/media/image15.png)

14. Under **By platform**, choose **Android**.

> ![](media/media/image16.png)

15. Select **Configuration profiles**.

> ![](media/media/image17.png)

16. Click **+ Create profile**.

> ![](media/media/image18.png)

17. Set the Platform to ***Android Enterprise***, choose ***Templates***
    as the profile type, select ***VPN*** as the template, and then
    click ***Create***.

![](media/media/image19.png)

18. On the Basics tab enter the following details and click **Next.**

- **Name:** Contoso – Android VPN Policy

- **Description:** Deploys VPN settings to Contoso Android users.  
  ![](media/media/image20.png)

19. On the Configuration tab choose the following options and click
    **Next**

> **Connection type – Microsoft Tunnel**
>
> **Connection Name - Contoso VPN**
>
> **Microsoft Tunnel site – Contoso secure access site**

![](media/media/image21.png)

20. On the Assignments tab, under included groups we can either select
    specific groups or select All users, choose **All users** and click
    **Next.**

![](media/media/image22.png)

21. On the Review + Create tab check all the details and click
    **Create.**

![](media/media/image23.png)

![](media/media/image24.png)

**Results**

After completing this lab, you will have:

- Created a VPN configuration profile for Android devices

- Assigned VPN policies to user/device groups

- Monitored VPN deployment and compliance

Contoso Android users can now securely access corporate resources
through an automatically configured VPN connection.
