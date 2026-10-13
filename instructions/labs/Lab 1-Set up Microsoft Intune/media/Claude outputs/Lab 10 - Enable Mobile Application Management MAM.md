# Lab 10 – Implement Mobile Application Management (MAM) Using App Protection Policies in Microsoft Intune

### Summary

In this lab, you will use Microsoft Intune to configure and test **Mobile Application Management (MAM)** for unmanaged (BYOD) mobile devices. You will create an **App Protection Policy**, configure **MAM Conditional Access**, sign in to Microsoft 365 apps on a personal device, and validate selective wipe capabilities. This lab focuses on protecting *corporate data within apps* without requiring full device enrollment.

### Prerequisites

The following labs must be completed before this lab:

- Lab 1 – Set up Microsoft Intune
- Lab 2 – Manage Microsoft Entra Device Registration
- Lab 3 – Configure and Manage Device Enrollment
- Lab 4 – Enroll Devices into Microsoft Intune

You will also need:

- A personal **Android** mobile device capable of installing apps from the Google Play Store and receiving MFA prompts. The device must **not** be enrolled in Intune.
- **Cindy White** licensed with **Enterprise Mobility + Security E5** and **Office 365 E5 (no Teams)** (completed in Lab 3).

## Exercise 1: Create an App Protection Policy (MAM) for BYOD Devices

### Scenario

The Contoso IT team is planning to allow employees to access Outlook, Teams, and OneDrive on their personal phones. However, corporate data must be protected using Intune Mobile Application Management (MAM). Cindy White will help validate that app data is being protected under MAM policies on her personal device.

The policy requirements are:

- Prevent saving corporate data to personal storage
- Prevent copy/paste outside corporate apps
- Require a PIN to open corporate apps
- Encrypt data at rest within the app
- Block access from jailbroken/rooted devices

### Task 1: Create the Contoso MAM Users group

App protection policies and Conditional Access policies apply to **users**, not devices. In this task, you create a user group for the MAM pilot and add Cindy White to it.

1. On **SEA-SVR1**, sign in to the **Microsoft Intune admin center** (**https://intune.microsoft.com**) as an admin.

    ![](media/media/image1.png)

2. In the left navigation pane, select **Groups**, and then select **New group**.

3. On the **New Group** page, enter the following information:

    - Group type: **Security**
    - Group name: **Contoso MAM Users**
    - Group description: **Users in scope for Mobile Application Management**
    - Membership type: **Assigned**

4. Under **Members**, select **No members selected**. Search for and select **Cindy White**, and then choose **Select**.

5. Select **Create**. Verify that the **Contoso MAM Users** group is displayed in the **All groups** list.

### Task 2: Create an App Protection Policy (Android)

1. In the Microsoft Intune admin center, in the left navigation pane, select **Apps**.

    ![](media/media/image2.png)

2. Under **Manage apps**, select **Protection**. Then, on the **Apps | Protection** page, click **+ Create** and select **Android**.

    ![](media/media/image3.png)

3. On the **Basics** page, enter the following and click **Next**:

    - Name: **Contoso MAM – Mobile App Protection**
    - Description: **App protection policy for BYOD devices.**

    ![](media/media/image4.png)

4. On the **Apps** tab, set **Target policy to** **All Microsoft Apps** and then click **Next**.

    ![](media/media/image5.png)

5. In the **Data protection** section, configure the following and click **Next**:

    - **Backup Org data to Android backup services** → *Block*
    - **Send org data to other apps** → *Policy managed apps*
    - **Save copies of org data** → *Block*
    - **Allow user to save copies to selected services** → *OneDrive for Business* and *SharePoint*
    - **Restrict cut, copy, and paste between other apps** → *Policy managed apps*
    - **Encrypt Org data** → *Require*
    - **Screen capture and Google Assistant** → *Block*

    ![](media/media/image6.png)

    ![](media/media/image7.png)

6. On the **Access requirements** page, set the following and click **Next**:

    - **PIN for access** → *Require*
    - **PIN type** → *Numeric*
    - **Biometrics instead of PIN for access** → *Allow*

    ![](media/media/image8.png)

7. On the **Conditional launch** page, under **Device conditions**, ensure **Jailbroken/rooted devices** is set to **Block access**, and then click **Next**.

    ![](media/media/image9.png)

8. On the **Assignments** page, under **Included groups**, select **Add groups**, select **Contoso MAM Users**, and click **Next**.

    ![](media/media/image10.png)

9. On the **Review + create** page, click **Create**.

    ![](media/media/image11.png)

    Your MAM App Protection Policy is now active.

    ![](media/media/image12.png)

## Exercise 2: Configure MAM Conditional Access

### Scenario

To ensure only protected apps can access corporate data, Contoso wants to require users to use applications covered by the MAM policy.

### Task 1: Create a MAM Conditional Access policy

1. Go to the **Microsoft Entra admin center** (**https://entra.microsoft.com**).

    ![](media/media/image13.png)

2. In the left menu, select **Entra ID** → **Conditional Access**.

    ![](media/media/image14.png)

3. On the **Conditional Access | Overview** page, select **+ Create new policy**.

    ![](media/media/image15.png)

4. Name the policy **Require APP for Mobile Access**.

5. Under **Users or agents (Preview)**, select **Select users and groups**, check **Users and groups**, and then select the **Contoso MAM Users** group.

    ![](media/media/image16.png)

6. Under **Target resources**, click **No target resources selected** and ensure **Resources (formerly cloud apps)** is selected. Then click **Select resources** and choose **Office 365**.

    ![](media/media/image17.png)

    ![](media/media/image18.png)

7. In the **Conditions** section, select **Device platforms**, set **Configure** to **Yes**, and choose **Android** as the selected platform.

    ![](media/media/image19.png)

8. Under **Grant**, select **Grant access**, and then select:

    - **Require app protection policy**

    ![](media/media/image20.png)

9. Set **Enable policy** to **On** and click **Create**.

    ![](media/media/image21.png)

    This enforces secure access only through apps protected by your policy.

    > **Note:** Allow about 10–15 minutes for the new app protection and Conditional Access policies to take effect before starting Exercise 3.

## Exercise 3: Test MAM Policy Enforcement on a Personal Device

### Scenario

Cindy will sign in to Outlook on her personal Android phone and confirm that Contoso data is protected inside the app, while the device itself stays unmanaged.

### Task 1: Install the required apps

1. On your personal **Android** device, open the **Google Play Store**.

2. Search for and install **Intune Company Portal**.

    > **Note:** On Android, Company Portal must be installed for app protection policies to apply. You do **not** need to open it or enroll the device.

3. Search for and install **Microsoft Outlook**.

### Task 2: Sign in and set up the app PIN

1. Open **Microsoft Outlook** and select **Add account**.

2. Sign in as **Cindy@M365xXXXXXXX.onmicrosoft.com** (substitute **XXXXXXX** with your tenant name) with the password **P@55w.rd1234**. Complete any MFA prompts.

3. When the message **Your organization is now protecting its data in this app** appears, select **OK**. If prompted to restart the app, close Outlook and open it again.

4. When prompted, create a numeric **app PIN** and confirm it.

    The PIN prompt confirms that the **PIN for access** setting from the app protection policy has been applied.

### Task 3: Validate data protection

1. In Outlook, open any email in Cindy's inbox. Select and copy some text from the email.

2. Open a personal app on the phone that is not managed by Contoso (for example, **Messages** or **Google Keep**) and try to paste the text.

    Notice that the paste is blocked or replaced with a message that your organization's data can't be pasted here.

3. Return to Outlook and try to take a screenshot of the email.

    Notice that the screenshot is blocked.

4. Open an email with an attachment (or send Cindy one from SEA-SVR1), open the attachment menu, and try to save the attachment to the phone's local storage.

    Notice that saving to the device is blocked and only **OneDrive for Business** or **SharePoint** are offered as save locations.

### Task 4: Validate MAM Conditional Access

1. On the Android device, open **Google Chrome** and go to **https://outlook.office.com**.

2. Sign in as **Cindy@M365xXXXXXXX.onmicrosoft.com**.

    Notice that access is blocked with a message that the app or browser is not approved. Chrome is not covered by the app protection policy, so Conditional Access blocks it. Only policy-protected apps such as Outlook (or Microsoft Edge) can reach Contoso mail.

### Task 5: Review app protection status in Intune

1. On **SEA-SVR1**, in the **Microsoft Intune admin center**, select **Apps** → **Monitor** → **App protection status**.

2. Select **Assigned users** and confirm that **Cindy White** is listed with the **Contoso MAM – Mobile App Protection** policy applied to **Outlook**.

    > **Note:** It can take a few minutes after Cindy's first sign-in for the status to appear.

## Exercise 4: Perform a selective wipe

### Scenario

Cindy reports that her personal phone has been lost. Contoso must remove corporate data from the apps on the phone without touching her personal data.

### Task 1: Create a selective wipe request

1. In the **Microsoft Intune admin center**, select **Apps** → **App selective wipe**.

2. Select **+ Create wipe request**.

3. Under **User**, select **Cindy White**. Under **Device**, select Cindy's Android device, and then select **Create**.

4. Verify that the wipe request is listed with a status of **Pending**.

### Task 2: Verify the selective wipe on the device

1. On the Android device, close **Outlook** completely and open it again.

2. Notice that Cindy's Contoso account and mail are removed from Outlook. Personal apps and data on the phone are not affected.

3. On **SEA-SVR1**, refresh the **App selective wipe** page and verify that the request status changes to **Completed**.

    > **Note:** The wipe is applied the next time the app checks in with Intune, which usually happens when the app is opened.

### Results

After completing this lab, you will have:

- Created and assigned an **App Protection Policy** to a user group
- Implemented **MAM Conditional Access** for Android
- Verified PIN, copy/paste, screenshot, and save-as restrictions in Outlook on an unmanaged device
- Confirmed that unprotected apps such as Chrome are blocked from corporate data
- Removed corporate data from a personal device with an **app selective wipe**
