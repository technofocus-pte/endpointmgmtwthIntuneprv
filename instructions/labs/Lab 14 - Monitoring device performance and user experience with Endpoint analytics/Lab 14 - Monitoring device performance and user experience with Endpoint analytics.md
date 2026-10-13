# Lab 14: Monitoring device performance and user experience with Endpoint analytics

### Summary

In this lab you enable Endpoint analytics to monitor device performance and user experience scores and insights.

### Prerequisites

The following lab(s) must be completed before this lab:

- Lab-Manage Device Enrollment into Intune
- Lab-Enrolling devices into Intune
- Lab-Creating and Deploying Configuration Profiles

### Scenario

You have been asked to monitor startup performance, application reliability, and how often users restart their devices. To acquire this information, you need to enable Endpoint analytics.

> **Note:** Endpoint analytics needs time to collect data. Scores and insights can take up to **24 hours** to appear after you enable it. In this lab you enable the feature, generate a restart on SEA-WS1, and learn where each report is found. If your lab environment is still running the next day, return to Task 2 to see the populated reports.

### Task 1: Enable Endpoint analytics

1. On **SEA-SVR1**, if necessary, sign in as **Contoso\Administrator** with the password **Pa55w.rd** and close **Server Manager**.

2. On the taskbar, select **Microsoft Edge**.

3. In Microsoft Edge, type **https://intune.microsoft.com** in the address bar, and then press **Enter**.

4. Sign in as **admin@M365xXXXXXXX.onmicrosoft.com** (substitute **XXXXXXX** with your tenant name) with the tenant admin password.

5. On the **Microsoft Intune admin center** page, select **Reports**.

6. On the **Reports** blade, under **Endpoint analytics**, select **Endpoint analytics**.

    ![](media/media/image1.png)

7. On the **Endpoint analytics** page, ensure that **Collect device data from** is set to **All cloud-managed devices**, and then select **Start**.

    ![](media/media/image2.png)

    Take note of the message at the top of the **Overview** page. It may take up to 24 hours for scores and insights to display on the page.

    ![](media/media/image3.png)

    > **Note:** Selecting **Start** creates the **Intune data collection policy** and assigns it to all cloud-managed devices, including SEA-WS1.

8. Switch to **SEA-WS1** and restart the device.

    The restart gives Endpoint analytics a boot and sign-in to measure for the **Startup performance** report.

9. Sign in as **Cindy White** with the PIN **102938**.

10. Switch to **SEA-SVR1**.

11. On the **Microsoft Intune admin center** page, select **Devices** and then select **All devices**.

12. Select **SEA-WS1**.

    ![](media/media/image4.png)

13. On the **SEA-WS1** page, select **Sync** and then select **Yes**.

    ![](media/media/image5.png)

    The sync makes sure SEA-WS1 receives the Intune data collection policy.

### Task 2: Review Endpoint analytics reports

1. On the **SEA-WS1** device page, under **Monitor**, select **User experience**.

    ![](media/media/image6.png)

2. Review the **Endpoint analytics**, **Startup performance**, and **Application reliability** tabs.

    ![](media/media/image7.png)

    ![](media/media/image8.png)

    ![](media/media/image9.png)

    There may not be any information reported yet due to the collection delay. Read the details on what will be visible on each tab.

3. On the **Microsoft Intune admin center** page, select **Reports**.

4. On the **Reports** blade, under **Endpoint analytics**, select **Endpoint analytics**.

    ![](media/media/image10.png)

    Note that the same type of information is available here, but it is based on all enrolled devices rather than a single device.

    ![](media/media/image11.png)

5. Browse through the reports available on the Endpoint analytics page, such as **Startup performance**, **Application reliability**, and **Work from anywhere**.

6. Close Microsoft Edge.

**Results**: After completing this exercise, you will have successfully enabled Endpoint analytics to monitor device performance and user experience scores and insights.
