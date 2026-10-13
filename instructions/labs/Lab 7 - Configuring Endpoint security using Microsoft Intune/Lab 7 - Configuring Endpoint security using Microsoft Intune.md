# Lab 7 - Configuring Endpoint security using Microsoft Intune

### Summary

In this lab, you will create a policy to configure Microsoft Defender for managed devices in Microsoft Intune.

### Prerequisites

The following lab(s) must be completed before this lab:

- Lab-Manage Device Enrollment into Microsoft Intune
- Lab-Enrolling devices into Microsoft Intune
- Lab-Create and Deploy Configuration Profiles

### Scenario

You've been asked to ensure that the Contoso Developers group has Microsoft Defender correctly configured. It's been requested that:

- Tamper protection be enabled.
- The Account protection, App and browser control, Device security, Device performance and health, and Family options areas be hidden in the Windows Security app.
- Company name and phone number must be added.
- Real-time protection, remediation, and scan settings are also to be configured.

Settings will be verified by testing on an enrolled device, SEA-WS1, and a non-enrolled device, SEA-CL1.

### Task 1: Configure Windows Security Experience in Intune

1. Switch to **SEA-SVR1** and sign in as **Contoso\Administrator** with the password **Pa55w.rd**.

2. On the taskbar, select **Microsoft Edge**.

3. In Microsoft Edge, type **https://intune.microsoft.com** in the address bar, and then press **Enter**.

4. Sign in as the Office 365 Tenant Admin.

    ![](media/media/image1.png)

5. From the navigation pane, select **Endpoint security**, then select **Antivirus**.

    ![](media/media/image2.png)

6. On the **Endpoint security | Antivirus** pane, select **+ Create Policy**.

    ![](media/media/image3.png)

7. In the **Create a profile** pane, for **Platform**, select **Windows**. In the **Profile** list, select **Windows Security experience**. Then select **Create**.

    ![](media/media/image4.png)

8. On the **Basics** tab, in the **Name** field, enter **Windows Security Settings**. Select **Next**.

    ![](media/media/image5.png)

9. Under **Defender**, configure the following setting:

    - TamperProtection (Device): **On**

    ![](media/media/image6.png)

10. Under **Windows Defender Security Center**, configure the following settings:

    - Disable Account Protection UI: **Enable**
    - Disable App Browser UI: **Enable**
    - Disable Device Security UI: **Enable**
    - Disable Family UI: **Enable**
    - Disable Health UI: **Enable**

    ![](media/media/image7.png)

11. Next to **Enable Customized Toasts**, select **Enable**.

12. In the **Company name** field, select **Configured**, and then enter **Contoso IT**.

13. For **Phone**, select **Configured**, enter **555-1234**, and then select **Next**.

    ![](media/media/image8.png)

14. On the **Scope tags** page, select **Next**.

    ![](media/media/image9.png)

15. On the **Assignments** tab, under **Included groups**, select **Add groups**. Choose the **Contoso Developer devices** group, click **Select** and then select **Next**.

    ![](media/media/image10.png)

16. On the **Review + create** tab, review the information and select **Save**.

    ![](media/media/image11.png)

### Task 2: Configure Microsoft Defender Antivirus policy in Intune

1. On the **Endpoint security | Antivirus** pane, select **+ Create Policy**.

    ![](media/media/image12.png)

2. In the **Create a profile** pane, for **Platform**, select **Windows**. In the **Profile** list, select **Microsoft Defender Antivirus**, then select **Create**.

    ![](media/media/image13.png)

3. On the **Basics** tab, in the **Name** field, enter **Microsoft Defender Antivirus Settings**. Select **Next**.

    ![](media/media/image14.png)

4. On the **Configuration settings** tab, configure the following settings:

    - Allow Intrusion Prevention System: **Allowed**
    - Allow scanning of all downloaded files and attachments: **Allowed**
    - Allow Realtime Monitoring: **Allowed**

    ![](media/media/image15.png)

    - Check For Signatures Before Running Scan: **Enabled**
    - Days to Retain Cleaned Malware: **60**

    ![](media/media/image16.png)

    - Schedule Quick Scan Time: **60** (represents 1:00 AM)

    ![](media/media/image17.png)

    - Submit Samples Consent: **Send safe samples automatically**

    ![](media/media/image18.png)

5. On the **Configuration settings** tab, select **Next**.

6. On the **Scope tags** page, select **Next**.

    ![](media/media/image19.png)

7. On the **Assignments** tab, under **Included groups**, select **Add groups**.

8. Choose the **Contoso Developer devices** group, choose **Select** and then select **Next**.

    ![](media/media/image20.png)

9. On the **Review + create** tab, review the information and select **Save**.

    ![](media/media/image21.png)

### Task 3: Sync the managed devices

1. In the **Microsoft Intune admin center**, select **Devices** and then select **All devices**.

2. On the **Devices | All devices** pane, select **SEA-WS1**. On the **SEA-WS1** blade, select **Sync** on the toolbar, and then select **Yes**.

    ![](media/media/image22.png)

    > **Note:** Wait 3-4 minutes for the sync to complete.

3. Close Microsoft Edge.

### Task 4: Verify the configuration

1. On your lab VM, select **Start**, type **Windows Security**, and then under the Windows Security icon select **Open**.

    ![](media/media/image23.png)

2. Notice the security options that are displayed.

    ![](media/media/image24.png)

3. Switch to **SEA-WS1**, and sign in as **Cindy@M365xXXXXXXX.onmicrosoft.com** with the password **P@55w.rd1234**.

4. Select **Start**, type **Windows Security**, and then under the Windows Security icon select **Open**.

    ![](media/media/image25.png)

    Notice that the restricted areas configured in the Intune policy are not displayed. **SEA-WS1** is enrolled in Intune, which has applied the security settings.

    ![](media/media/image26.png)

5. Close **Windows Security** and sign out of **SEA-WS1**.

**Results**: After completing this exercise, you will have successfully created and applied a policy to configure Microsoft Defender for managed devices in Intune.
