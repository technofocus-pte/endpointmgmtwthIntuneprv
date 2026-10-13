# Lab 8: Configure Update Management

### Summary

In this lab you will configure Windows quality and feature update settings using Intune.

### Prerequisites

The following lab(s) must be completed before this lab:

- Lab-Set up Microsoft Intune
- Lab-Enrolling devices into Intune
- Lab-Creating and Deploying Configuration Profiles

> **Note:** You will also need a mobile phone that can receive text messages used to secure Windows Hello sign-in authentication to Microsoft Entra ID.

### Scenario

You have been asked to configure an update ring to only affect the devices that are members of the Contoso Developer devices group. This group must meet the following requirements:

- Quality update deferral period (days): **15**
- Feature update deferral period (days): **45**
- Option to pause Windows updates: **Disable**
- Option to check for Windows updates: **Enable**
- Delivery optimization: Download Mode: **HTTP only, no peering (0)**

### Task 1: Verify current update settings for a single device

1. Switch to **SEA-WS1**, and sign in as **Cindy White** with the PIN **102938**.

2. Select **Start**, and then select the **Settings** icon.

    ![](media/media/image1.png)

3. In **Settings**, select **Windows Update**.

    Notice that you have the option to pause updates for a specific amount of time.

4. On the **Windows Update** page, select **Advanced options**.

    ![](media/media/image2.png)

5. On the **Advanced options** page, select **Delivery Optimization**.

    ![](media/media/image3.png)

6. On the **Delivery Optimization** page, verify that the **Allow downloads from other PCs** option is enabled.

7. Select **Devices on the internet and my local network**.

    ![](media/media/image4.png)

8. In **Settings**, select **Windows Update**.

    ![](media/media/image5.png)

9. Select **Advanced options**, and then select **Configured update policies**.

    ![](media/media/image6.png)

    Take note that no update policies are set on the device.

    ![](media/media/image7.png)

10. In the navigation pane, select **Windows Update**.

### Task 2: Review applied settings

1. On the **Windows Update** page, select **Update history**.

    ![](media/media/image8.png)

2. Review the updates listed, and then select **Uninstall updates**.

    ![](media/media/image9.png)

3. Review the updates listed in **Installed Updates**. Close **Installed Updates**.

    ![](media/media/image10.png)

4. Close the **Settings** app.

### Task 3: Configure update settings by using Intune

1. Switch to **SEA-SVR1** and sign in as **Contoso\Administrator** with the password **Pa55w.rd**.

2. On the taskbar, select **Microsoft Edge**.

3. In Microsoft Edge, type **https://intune.microsoft.com** in the address bar, and then press **Enter**.

4. Sign in as **admin@M365xXXXXXXX.onmicrosoft.com** with the tenant admin password.

5. In the navigation pane, select **Devices** and then, under **Manage updates**, select **Windows updates**.

    ![](media/media/image11.png)

6. On the **Devices | Update rings** blade, select **Create profile**.

    ![](media/media/image12.png)

7. On the **Basics** blade, enter the following information, and then select **Next**:

    - Name: **Contoso Updates - standard**
    - Description: **Standard Windows updates configuration**

    ![](media/media/image13.png)

8. On the **Update ring settings** blade, enter the following information, and then select **Next**:

    - Quality update deferral period (days): **15**
    - Feature update deferral period (days): **45**
    - Option to pause Windows updates: **Disable**
    - Option to check for Windows updates: **Enable**

    ![](media/media/image14.png)

9. On the **Assignments** blade, under **Included groups**, select **Add groups**.

    ![](media/media/image15.png)

10. On the **Select groups to include** blade, in the **Search** box, select **Contoso Developer devices** and then click **Select**.

    ![](media/media/image16.png)

11. Select **Next** and, on the **Review + create** blade, select **Create**.

    ![](media/media/image17.png)

    ![](media/media/image18.png)

12. From the navigation bar, under **Manage devices**, select **Configuration**.

    ![](media/media/image19.png)

13. On the **Devices | Configuration** blade, in the details pane, select **Create policy**.

    ![](media/media/image20.png)

14. In the **Create a profile** blade, select the following options, and then select **Create**:

    - Platform: **Windows 10 and later**
    - Profile type: **Templates**
    - Template name: **Delivery Optimization**

    ![](media/media/image21.png)

15. On the **Basics** blade, enter the following information, and then select **Next**:

    - Name: **Contoso Developer - Delivery optimization**
    - Description: **Delivery optimization for Developer**

    ![](media/media/image22.png)

16. On the **Configuration settings** blade, enter the following information, and then select **Next**:

    - DO Download Mode: **HTTP only, no peering (0)**

    ![](media/media/image23.png)

17. On the **Scope tags** tab, click **Next**.

18. On the **Assignments** blade, click on the search bar, select **Contoso Developer devices**, and then click **Next**.

    ![](media/media/image24.png)

    ![](media/media/image25.png)

19. On the **Review + create** blade, select **Save**.

    ![](media/media/image26.png)

    ![](media/media/image27.png)

    > **Note:** A manual sync can also be triggered from the Microsoft Intune portal to ensure the new configuration is applied to SEA-WS1.

    ![](media/media/image28.png)

### Task 4: Verify that the device's update settings are managed centrally

1. Switch to **SEA-WS1**.

2. Select **Start**, and then select the **Settings** icon.

    ![](media/media/image29.png)

3. In the **Settings** app, select **Accounts** and then select **Access work or school**.

    ![](media/media/image30.png)

4. In the **Access work or school** section, select **Connected to Contoso's Azure AD** and then select **Info**.

    ![](media/media/image31.png)

5. In the **Areas managed by Contoso** dialog box, select **Sync**. Wait for the synchronization to complete.

    ![](media/media/image32.png)

6. In the **Settings** app, select **Windows Update**. Notice that you are not able to pause updates.

    ![](media/media/image33.png)

7. Select **Advanced options**.

    ![](media/media/image34.png)

8. Select **Delivery Optimization**.

    ![](media/media/image35.png)

    Notice that **Allow downloads from other PCs** is not available.

    ![](media/media/image36.png)

9. In the **Settings** app, select **Windows Update**, select **Advanced options**, and then select **Configured update policies**.

    ![](media/media/image37.png)

    Take note of all the policies set on the device.

    ![](media/media/image38.png)

10. Close all open apps and windows.

> **Note:** The lab environment is configured to prevent Windows Updates from being applied to avoid delays and unintentional impact during the labs.
