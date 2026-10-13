# Lab 17 - Configuring and validating device compliance

### Summary

In this lab, you validate device compliance by configuring a compliance policy and an associated Conditional Access policy that uses the compliance status of a managed device to allow or block access to email.

### Prerequisites

The following lab(s) must be completed before this lab:

- Lab #1-Set up Microsoft Intune
- Lab #3-Manage Device Enrollment into Microsoft Intune
- Lab #4-Enrolling devices into Microsoft Intune
- Lab #6-Creating and Deploying Configuration Profiles

> **Note:** This lab uses the **Windows Devices** dynamic group created in Lab 6, and **Cindy White**, who was licensed for Exchange Online in Lab 3 and enrolled **SEA-WS1** in Lab 4.

## Exercise 1: Configuring compliance policies

### Scenario

Contoso would like to ensure that Windows devices that are enrolled in Microsoft Intune meet a minimum configuration specification. The following specifications are required:

- Minimum Windows operating system version: **10.0.19041.329**
- Microsoft Defender Antimalware: **Required**

If a device meets these requirements, it will be marked as compliant. If the device does not meet these requirements, the device should be marked as noncompliant.

### Task 1: Create and assign a compliance policy

1. Sign in to **SEA-SVR1** as **Contoso\Administrator** with the password **Pa55w.rd**.

2. On the taskbar, select **Microsoft Edge**. In Microsoft Edge, type **https://intune.microsoft.com** in the address bar, and then press **Enter**.

3. Sign in with the **Office 365 Tenant Admin** credentials.

    ![](media/media/image1.png)

4. From the navigation pane, select **Devices**, then select **Compliance** under **Manage devices**.

    ![](media/media/image2.png)

5. On the **Compliance | Policies** blade, in the details pane, select **+ Create policy**.

    ![](media/media/image3.png)

6. On the **Create a policy** blade, provide the following value and select **Create**:

    - Platform: **Windows 10 and later**

    ![](media/media/image4.png)

7. On the **Basics** tab, provide the following value and select **Next**:

    - Name: **Compliance1**

    ![](media/media/image5.png)

8. On the **Compliance settings** tab, expand **Device Health** and review the available settings.

    ![](media/media/image6.png)

9. On the **Compliance settings** tab, expand **Device Properties**. In the **Minimum OS version** field, type **10.0.19041.329**.

    ![](media/media/image7.png)

10. On the **Compliance settings** tab, expand **System Security**. Set the **Microsoft Defender Antimalware** setting to **Require** and then select **Next**.

    ![](media/media/image8.png)

11. On the **Actions for noncompliance** tab, note that the default action **Mark device noncompliant** is set to **Immediately**.

    ![](media/media/image9.png)

    Review how you can configure the number of days after which the device is marked as noncompliant, and configure additional actions.

12. Select **Next**. On the **Assignments** tab, select **Add groups**. Select **Windows Devices**, choose **Select**, and then select **Next**.

    ![](media/media/image10.png)

    > **Note:** The **Windows Devices** dynamic group was created in Lab 6 and automatically includes SEA-WS1.

13. Select **Create**.

    ![](media/media/image11.png)

14. In the navigation menu, select **Devices**, and then in the Devices navigation pane, select **Compliance**.

    ![](media/media/image12.png)

15. On the **Compliance** page, select **Compliance settings**.

    ![](media/media/image13.png)

16. On the **Compliance policy settings** page, next to **Mark devices with no compliance policy assigned as**, select **Not compliant** and then select **Save**.

    ![](media/media/image14.png)

    This setting ensures that any device that does not have a compliance policy assigned will be set to **Not compliant**.

### Task 2: Evaluate compliance on SEA-WS1

Before you enforce compliance with Conditional Access, confirm that SEA-WS1 has been evaluated as compliant.

1. Switch to **SEA-WS1** and sign in as **Cindy White** with the PIN **102938**.

2. Select **Start** → **Settings** → **Accounts** → **Access work or school**. Select **Connected to Contoso's Azure AD** → **Info**, scroll down, and select **Sync**.

3. Switch to **SEA-SVR1**. In the **Microsoft Intune admin center**, select **Devices** → **All devices**.

4. Find **SEA-WS1** and verify that the **Compliance** column shows **Compliant**.

    > **Note:** The first compliance evaluation can take 10–15 minutes. If SEA-WS1 shows **Not evaluated** or **In grace period**, wait a few minutes, select **Refresh**, and check again. Do not continue to Exercise 2 until SEA-WS1 shows **Compliant**, or Cindy will be blocked on SEA-WS1 too.

**Results**: After completing this exercise, you will have successfully configured a compliance policy and verified that SEA-WS1 is compliant.

## Exercise 2: Creating a Conditional Access policy to enforce compliance

### Scenario

When a user uses a device that is not marked as compliant, they should not be able to access their email. You've been asked to configure a Conditional Access policy that enforces this rule, and verify that it functions as expected.

### Task 1: Create a Conditional Access policy

1. On **SEA-SVR1**, in the **Microsoft Intune admin center**, select **Devices**, then select **Conditional access**.

    ![](media/media/image15.png)

2. Select **Policies**, then select **+ New policy**.

    ![](media/media/image16.png)

3. On the **New** blade, in the **Name** text box, type **Conditional1**, and then select **0 users or workload identities selected**.

    ![](media/media/image17.png)

4. On the **Include** tab, select **Select users and groups**, select the **Users and groups** check box, search for and select **Cindy White**, and then choose **Select**.

    ![](media/media/image18.png)

    > **Note:** The policy targets only Cindy so that it cannot lock the tenant admin or other lab users out of Exchange Online.

5. On the **New** blade, select **No target resources selected**, select the **Select resources** radio button, select **Office 365 Exchange Online**, and then click **Select**.

    ![](media/media/image19.png)

6. On the **New** blade, in the **Conditions** section, select **0 conditions selected**.

    ![](media/media/image20.png)

7. In the list of conditions, under **Device platforms**, select **Not configured**. Set **Configure** to **Yes**, select the **Select device platforms** radio button, select the **Windows** check box, and then select **Done**.

    ![](media/media/image21.png)

8. On the **New** blade, under **Access controls**, in the **Grant** section, select **0 controls selected**.

9. Select **Grant access**, select the **Require device to be marked as compliant** check box, and then select **Select**.

    ![](media/media/image22.png)

10. On the **New** blade, set **Enable policy** to **On** and then select **Create**.

    ![](media/media/image23.png)

    > **Note:** Allow about 5 minutes for the new policy to take effect before testing.

### Task 2: Verify that access is blocked from an unmanaged device

SEA-SVR1 is a Windows device that is **not** enrolled in Intune, so it has no compliance status. You use it to test what happens when Cindy signs in from an unmanaged device.

1. On **SEA-SVR1**, in Microsoft Edge, press **Ctrl+Shift+N** to open an **InPrivate** window.

2. In the InPrivate window, go to **https://outlook.office.com**.

3. Sign in as **Cindy@M365xXXXXXXX.onmicrosoft.com** (substitute **XXXXXXX** with your tenant name) with the password **P@55w.rd1234**.

    ![](media/media/image24.png)

4. Verify that access is blocked, and that you receive a message that the device does not meet your organization's requirements, such as **You can't get there from here**.

    ![](media/media/image25.png)

5. Select **More details**. You should see more information about why you are blocked.

    ![](media/media/image26.png)

    > **Note:** Cindy is blocked because SEA-SVR1 is not joined to Microsoft Entra ID and not managed by Microsoft Intune, so it is not marked as compliant.

6. Close the InPrivate window.

### Task 3: Verify that access is allowed from a compliant device

1. Switch to **SEA-WS1**, and sign in as **Cindy White** with the PIN **102938**.

    > **Note:** SEA-WS1 is a managed Windows 11 device that is enrolled in Intune and marked as compliant.

2. On the taskbar, select **Microsoft Edge**. In Microsoft Edge, type **https://outlook.office.com** and then press **Enter**.

3. If prompted, sign in as **Cindy@M365xXXXXXXX.onmicrosoft.com**. Verify that you can access Cindy's mailbox.

    ![](media/media/image27.png)

    > **Note:** Cindy is allowed because **SEA-WS1** is a managed device that is marked as compliant.

4. Close Microsoft Edge and sign out of **SEA-WS1**.

### Task 4: Disable the Conditional Access policy

1. On **SEA-SVR1**, in the **Microsoft Intune admin center**, select **Devices**, then select **All devices**.

    ![](media/media/image28.png)

    Notice that **SEA-WS1** is compliant, which is why Cindy was allowed to access her mailbox.

2. From the navigation pane, select **Devices**, then select **Conditional access**.

    ![](media/media/image29.png)

3. On the **Conditional Access** page, select **Policies**, then select **Conditional1**.

    ![](media/media/image30.png)

4. On the **Conditional1** page, at the bottom of the page, select **Off** and then select **Save**.

    ![](media/media/image31.png)

5. Close Microsoft Edge.

**Results**: After completing this exercise, you will have successfully configured a Conditional Access policy that uses device compliance to control access to email.
