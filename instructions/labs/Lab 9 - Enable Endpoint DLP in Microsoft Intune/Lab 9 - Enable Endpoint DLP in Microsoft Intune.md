# Lab 9 – Enable Endpoint Data Loss Prevention (Endpoint DLP) in Microsoft Purview

**Summary**

In this lab, you will enable and configure **Endpoint Data Loss
Prevention (Endpoint DLP)** in the new Microsoft Purview portal. You
will onboard Windows 11 devices using Intune, create DLP policies,
monitor user activity, and enforce endpoint restrictions such as
blocking sensitive data uploads, copying to USB drives, and accessing
classified content from untrusted applications.

Endpoint DLP helps Contoso prevent data leakage from devices without
requiring a full MDM solution and works seamlessly with Microsoft 365
data classification.

------------------------------------------------------------------------

**Prerequisites**

Before starting this lab, ensure the following labs are completed:

- Lab 1 – Set up Microsoft Intune

- Lab 2 – Manage Entra Device Registration

- Lab 3 – Configure Device Enrollment

- Lab 4 – Enroll Windows Devices into Intune

- Lab 5 – Integrate Microsoft Defender for Endpoint with Intune

- SEA‑WS1 enrolled in Intune and successfully onboarded to Microsoft
  Defender for Endpoint

------------------------------------------------------------------------

## Exercise 1: Enable Endpoint DLP in Microsoft Purview

**Scenario**

Contoso wants to extend its Microsoft Purview DLP protection to Windows
11 endpoints to prevent accidental data leakage. Before you can apply
Endpoint DLP policies, you must enable and configure endpoint
onboarding.

------------------------------------------------------------------------

### Task 1: Enable Endpoint DLP in the Purview Portal

1.  Sign in to **Microsoft Purview portal**  
    <https://purview.microsoft.com>

> ![](media/media/image1.png)

2.  Click Settings then Select **Endpoint DLP settings**.

> ![](media/media/image2.png)
>
> ![](media/media/image3.png)

3.  Enable the following:

    - **Enable advanced classification scanning and protection** → *On*

> ![](media/media/image4.png)

------------------------------------------------------------------------

## Exercise 2: Onboard Windows 11 Devices to Endpoint DLP (via Intune)

**Scenario**

Endpoint DLP requires the Microsoft Defender for Endpoint sensor. Since
SEA‑WS1 was already onboarded in Lab 5, you will now verify Endpoint DLP
onboarding.

### Task 1: Verify Endpoint DLP Onboarding in Intune

1.  Go to the **Microsoft Intune admin center**.

2.  Navigate to:  
    **Endpoint security → Microsoft Defender for Endpoint**

3.  Verify that the connection status for **Microsoft Defender for
    Endpoint** is enabled.

> ![](media/media/image5.png)

4.  Under **Endpoint Security Profile Settings** enable**-** Allow
    Microsoft Defender for Endpoint to enforce Endpoint Security
    Configurations 

5.  Under **Compliance policy evaluation** enable- Connect Windows
    devices version 10.0.15063 and above to Microsoft Defender for
    Endpoint 

> ![](media/media/image6.png)

------------------------------------------------------------------------

## Exercise 3: Create an Endpoint DLP Policy

**Scenario**

The Contoso Compliance Team requires a new Endpoint DLP policy to
protect customer financial information and prevent users from copying,
printing, or uploading sensitive data from their laptops.

This policy will protect:

- Credit card numbers

- Financial identifiers

- Company confidential documents

------------------------------------------------------------------------

### Task 1: Create a DLP Policy in Purview

1.  In Microsoft Purview, navigate to:  
    **Data loss prevention → Policies → + Create policy**

> ![](media/media/image7.png)

2.  Select Enterprise applications & devices.

3.  ![](media/media/image8.png)

4.  Choose the template: **Financial data – U.S. Financial Data** (or
    All Sensitive Data Types)

> ![](media/media/image9.png)

5.  Click **Next**.

6.  Enter the **Name & Description** and click **Next.**

- Name: **Contoso – Endpoint DLP Policy**

- Description: **Protects sensitive data on Windows 11 endpoints**

Click **Next**.

> ![](media/media/image10.png)

7.  On the Assign admin units page, click **Next.**

![](media/media/image11.png)

8.  Under Locations, enable the following and click **Next.**

- **Devices** (mandatory for Endpoint DLP)

- Optionally also enable:

  - Exchange

  - SharePoint

  - Teams chat and channel messages

![](media/media/image12.png)

9.  On the Define policy settings page, select **Review and customize
    default settings from the template.**

![](media/media/image13.png)

10. On the protection actions page, modify the detection to match at
    least 1 sensitive info and click **Next.**

> ![](media/media/image14.png)

11. On the Policy mode page click on the radio button for **Turn the
    policy on immediately.**

![](media/media/image15.png)

12. Click **Submit.**

![](media/media/image16.png)

![](media/media/image17.png)

13. On the policy is created we will now navigate to **Solutions 🡪
    Audit**. Click on Start **recording user and admin activity.**

![](media/media/image18.png)

------------------------------------------------------------------------

------------------------------------------------------------------------

## Exercise 4: Test Endpoint DLP on SEA‑WS1

**Scenario**

Cindy will test Endpoint DLP by attempting to copy or upload sensitive
data on teams.

------------------------------------------------------------------------

### Task 1: Prepare a Test Sensitive Document

1.  On SEA‑WS1, open teams by navigating to the following url  
    <https://teams.microsoft.com>.

2.  Start trail to use teams to check the DLP policy for endpoints.

> ![](media/media/image19.png)

3.  Send a message with the following sample sensitive content, to a
    team member

> **Credit Card: 4111-1111-1111-1111**
>
> **Bank Routing No: 021000021**

![](media/media/image20.png)

4.  Notice that the message gets flagged

![](media/media/image21.png)

![](media/media/image22.png)

![](media/media/image23.png)

------------------------------------------------------------------------

## Exercise 5: Validate DLP Alerts and Activity Logs

### Task 1: Review Events in Purview Activity Explorer

1.  Go to:  
    **Microsoft Purview → Data loss prevention → Activity explorer**

2.  Go to:  
    **Purview → Data loss prevention → Alerts**

3.  Review alerts triggered by Cindy.

------------------------------------------------------------------------

**Results**

After completing this lab, you have successfully:

- Enabled Endpoint DLP using the new Microsoft Purview interface

- Onboarded Windows 11 devices for Endpoint DLP

- Tested Endpoint DLP user experience

- Validated alerts and activity logs in Purview

Your Contoso environment now has strong **endpoint data protection**
fully integrated with Microsoft 365 and Intune.

------------------------------------------------------------------------
