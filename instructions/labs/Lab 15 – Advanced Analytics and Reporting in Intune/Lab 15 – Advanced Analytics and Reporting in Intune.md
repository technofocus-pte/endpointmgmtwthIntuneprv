# Lab 15 – Advanced Analytics and Reporting in Intune

### Summary

In this lab, you will explore and use the **advanced analytics and reporting capabilities** in Microsoft Intune. You will work with Intune's reporting solutions—including **Endpoint analytics**, **device reports**, **app reports**, **compliance reporting**, and **audit logs**—to understand how administrators can monitor device health, track user experience, measure compliance, and gain insights into the organization's endpoint environment.

### Prerequisites

Before beginning this lab, ensure the following labs are completed:

- Lab 3 – Manage Device Enrollment into Intune
- Lab 4 – Enrolling Devices into Intune
- Lab 6 – Creating and Deploying Configuration Profiles
- Lab 14 – Monitoring Device Performance with Endpoint Analytics *(recommended)*

You must also have:

- **SEA-WS1** enrolled in Intune
- Admin access to the Intune admin center

> **Note:** The reports in this lab show the policies, apps, and devices you created in earlier labs. The more labs you have completed, the more data you will see. Reports that have no data yet will show an empty list — that is expected.

### Scenario

Contoso wants to strengthen visibility across all managed devices. Leadership is requesting reports on:

- Device performance
- User experience
- App performance and installation status
- Device compliance posture
- Security configuration drift
- Audit and administrative activity

As an Intune administrator, you will explore the **advanced analytics and reporting** features to gather this information.

## Exercise 1: Explore Intune Reporting Overview

### Task 1: Access the Reports workspace

1. On **SEA-SVR1**, sign in to the **Microsoft Intune admin center** (**https://intune.microsoft.com**) as the tenant admin.

    ![](media/media/image1.png)

2. In the left navigation pane, select **Reports**.

    ![](media/media/image2.png)

3. Review the reporting categories:

    - **Device management**
    - **Endpoint security**
    - **Analytics**

    ![](media/media/image3.png)

### Task 2: Review Endpoint analytics reports

1. In the Intune admin center, go to **Reports → Endpoint analytics**.

    ![](media/media/image4.png)

2. If you completed Lab 14, Endpoint analytics is already enabled and you can skip to the next step. Otherwise, for **Collect device data from**, ensure that **All cloud-managed devices** is selected and click **Start**.

    ![](media/media/image5.png)

    > **Note:** If Endpoint analytics was only just enabled, scores can take up to 24 hours to appear.

3. Explore the available insights:

    - **Startup performance**
    - **Application reliability**
    - **Work from anywhere**
    - **Battery health** (if applicable)

    ![](media/media/image6.png)

    ![](media/media/image7.png)

    ![](media/media/image8.png)

    ![](media/media/image9.png)

    Endpoint analytics helps evaluate how device performance affects user productivity.

## Exercise 2: Review Device and Compliance Reports

### Task 1: Device compliance reports

1. Navigate to **Reports → Device management → Device compliance**.

    ![](media/media/image10.png)

2. On the **Summary** tab, review the compliance status of your devices. Then select the **Reports** tab and review the available reports, such as **Device compliance** and **Noncompliant devices and settings**.

    ![](media/media/image11.png)

    > **Note:** This course does not create a compliance policy, so SEA-WS1 is evaluated against the tenant's default compliance setting. Its status reflects the **Mark devices with no compliance policy assigned as** setting under **Endpoint security → Device compliance → Compliance settings**.

### Task 2: Device configuration reports

1. Navigate to **Reports → Device management → Device configuration**.

2. Select the **Reports** tab, open the **Profile configuration status** report, and select **Generate report**.

3. Find the **Contoso Developer - standard** profile from Lab 6 and review:

    - Deployment status (succeeded, error, conflict)
    - Policy conflict details
    - Per-device configuration results

    ![](media/media/image12.png)

    This is critical for troubleshooting devices with configuration failures.

## Exercise 3: Analyze App Reports

### Task 1: Review managed app installation status

1. Go to **Apps → Monitor**, and select **App install status**.

    ![](media/media/image13.png)

    ![](media/media/image14.png)

2. Review the following for each app:

    - Installation success
    - Pending installations
    - Failed installations
    - Platform-based filters (Windows, iOS, Android)

    ![](media/media/image15.png)

3. If any app shows failed installations, select it, select **Device install status**, and review the error code for the failed device. If no app has failures, select **7-Zip** (from Lab 12), if present, and review its device install status instead.

4. If you completed Lab 10, return to **Apps → Monitor** and select **App protection status** to review the app protection report for Cindy White.

## Exercise 4: Explore Security and Endpoint Reporting

### Task 1: Endpoint security reports

1. Navigate to **Endpoint security → Antivirus**.

    ![](media/media/image16.png)

2. Review the **Summary** tab, and then the reports for:

    - **Unhealthy endpoints**
    - **Active malware**

3. Navigate to **Reports → Endpoint security → Firewall** and review the **MDM firewall status for Windows 10 and later** report to validate firewall status.

    ![](media/media/image17.png)

## Exercise 5: Use Audit Logs and Operational Data

### Task 1: Audit logs

1. Go to **Tenant administration → Audit logs**.

    ![](media/media/image18.png)

2. Review log activities from the earlier labs, such as:

    - Policy changes (for example, creating **Contoso Developer - standard**)
    - App deployments (for example, adding **7-Zip**)
    - Assignment changes

3. Select any entry to view details such as **Initiated by**, **Activity**, and the old and new values that were changed.

### Task 2: Diagnose operational issues

1. Navigate to **Tenant administration → Device diagnostics**.

2. Review the settings available for collecting diagnostics, and ensure that **Device diagnostics** is set to **Enabled**.

    ![](media/media/image19.png)

3. Go to **Devices → All devices**, select **SEA-WS1**, and select **Collect diagnostics** on the toolbar. Select **Yes** to confirm.

4. On the **SEA-WS1** page, select **Device diagnostics** under **Monitor**. Wait for the collection status to change to **Complete** (this can take 15–30 minutes), and then select **Download** to review the collected logs.

### Results

After completing this lab, you will have:

- Explored Intune's reporting workspace
- Reviewed Endpoint analytics performance data
- Reviewed compliance, configuration, and device status reports
- Analyzed application deployment and app protection reports
- Examined security posture and antivirus reporting
- Used audit logs and device diagnostics for operational tracking

Contoso now benefits from improved visibility into device performance, app reliability, and compliance across all managed endpoints.
