# Lab 20 - Using a Configuration Profile to configure iOS and iPadOS Wi-Fi settings

### Summary

In this lab, we will use Microsoft Intune to create and assign a Configuration profile that configures Wi-Fi settings for iOS and iPadOS devices.

### Prerequisites

The following lab(s) must be completed before this lab:

- Lab #1-Set up Microsoft Intune

> **Note:** This lab creates and assigns the Wi-Fi profile in Intune. Delivering it to a device requires an iPhone or iPad enrolled in Intune, which in turn requires an Apple MDM push certificate. Neither is part of this lab environment, so you will create and assign the profile and review where its deployment status is reported, without connecting a device.

## Exercise 1: Creating a Configuration profile

### Scenario

You have been asked to create a Configuration profile to automatically configure the corporate Wi-Fi network on enrolled iOS and iPadOS devices, so that users don't have to enter the network details themselves. You need to ensure that the Wi-Fi settings are configured as follows:

- Network name: **Contoso Corporate**
- SSID: **Contoso-Corp**
- Connect automatically: **Enabled**
- Security type: **WPA/WPA2-Personal**
- Pre-shared key: **C0ntos0-WiFi-2026**

### Task 1: Create the iOS_iPadOS Devices group

1. Switch to **SEA-SVR1**. In the **Microsoft Intune admin center** window, select **Groups**, then click **New group**.

    ![](media/media/image1.png)

2. On the **New Group** blade, enter the following information and click the **Create** button:

    - Group type: **Security**
    - Group name: **iOS_iPadOS Devices**
    - Group description: **All iOS and iPadOS devices**
    - Membership type: **Assigned**

    ![](media/media/image2.png)

    > **Note:** The group is created empty. In production, you add enrolled iPhones and iPads to it, or use **Dynamic Device** membership with the rule `(device.deviceOSType -eq "iPhone") or (device.deviceOSType -eq "iPad")` so that new devices are added automatically.

3. On the **Groups | All groups** blade, refresh the page and verify that the **iOS_iPadOS Devices** group is displayed.

    ![](media/media/image3.png)

### Task 2: Create a Configuration profile based on scenario requirements

1. Switch to the **Microsoft Intune admin center** tab and select **Devices** from the navigation bar.

2. On the **Devices | Overview** page, select **iOS/iPadOS** as shown in the below image.

    ![](media/media/image4.png)

3. On the **iOS/iPadOS** page, navigate and click on **Configuration profiles**.

    ![](media/media/image5.png)

4. On the **iOS/iPadOS | Configuration profiles** page, in the **Policies** tab, click **+ Create** and select **+ New Policy**.

    ![](media/media/image6.png)

5. In the **Create a profile** blade, select the following options, and then select **Create**:

    - Platform: **iOS/iPadOS**
    - Profile type: **Templates**
    - Template name: **Wi-Fi**

6. On the **Basics** blade, enter the following information, and then select **Next**:

    - Name: **iOS/iPadOS Wi-Fi Policy**
    - Description: **Corporate Wi-Fi settings for iOS/iPadOS devices**

7. On the **Configuration settings** blade, next to **Wi-Fi type**, select **Basic**.

    Additional options display based upon the type selected.

8. On the **Configuration settings** blade, configure the following options, and then select **Next**:

    - Network name: **Contoso Corporate**
    - SSID: **Contoso-Corp**
    - Connect automatically: **Enable**
    - Hidden network: **Disable**
    - Security type: **WPA/WPA2-Personal**
    - Pre-shared key: **C0ntos0-WiFi-2026**
    - Proxy settings: **None**

    > **Note:** **Network name** is the name users see on the device. **SSID** is the actual broadcast name of the wireless network and is case-sensitive.

9. On the **Assignments** blade, under **Included groups**, select **Add groups**.

    ![](media/media/image10.png)

10. In the **Select groups to include** window, select **iOS_iPadOS Devices**, and then click **Select**.

    ![](media/media/image11.png)

11. On the **Assignments** tab, click the **Next** button.

    ![](media/media/image12.png)

12. On the **Review + create** tab, review the settings and click the **Create** button.

    ![](media/media/image13.png)

13. Verify that the **iOS/iPadOS Wi-Fi Policy** is listed on the **iOS/iPadOS | Configuration profiles** page.

### Task 3: Review the profile deployment status

1. On the **iOS/iPadOS | Configuration profiles** page, select **iOS/iPadOS Wi-Fi Policy**.

2. On the profile **Overview** page, review the **Device and user check-in status** chart, and confirm under **Properties** that the profile is assigned to **iOS_iPadOS Devices**.

    > **Note:** Because no iOS or iPadOS devices are enrolled in this lab environment, the counts show **0**. When an enrolled device in **iOS_iPadOS Devices** checks in, it appears here as **Succeeded**, **Error**, or **Conflict**, and the **Contoso Corporate** network is added to the device's Wi-Fi settings.

**Results**: After completing this exercise, you will have successfully created and assigned a Configuration profile to configure Wi-Fi settings for iOS and iPadOS devices.
