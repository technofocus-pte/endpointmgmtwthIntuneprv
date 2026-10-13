# Lab 18: Configure App Protection Policies for Mobile Devices

### Summary

In this lab, you will configure an App protection policy for iOS/iPadOS devices and assign it to the users who need it.

### Prerequisites

The following lab(s) must be completed before this lab:

- Lab #1-Set up Microsoft Intune
- Lab #3-Manage Device Enrollment into Microsoft Intune
- Lab #10-Enable Mobile Application Management (MAM) *(recommended — creates the **Contoso MAM Users** group)*

Optional: an iPhone or iPad with **Microsoft Outlook** installed, if you want to test the policy on a device (Task 3).

### Scenario

All of the developers at Contoso have iPhones and iPads running the latest iOS/iPadOS versions. The security department is concerned with data leaks and wants to prevent data from the corporate email from being copied out to other apps on the mobile devices. You must provide a solution that addresses the concerns from the security department. You need to ensure the following:

- Outlook data must be restricted from backing up to iTunes or iCloud.
- Only policy managed apps can send and receive data from Outlook.
- Only policy managed apps can cut, copy, or paste with Outlook.
- Users must provide their work or school account credentials for access to Outlook.

### Task 1: Create an App protection policy for iOS/iPadOS devices

1. On **SEA-SVR1**, if necessary, sign in as **Contoso\Administrator** with the password **Pa55w.rd**.

2. On the taskbar, select **Microsoft Edge**, type **https://intune.microsoft.com** in the address bar, and then press **Enter**.

3. Sign in with the Office 365 Tenant admin credentials from the Home tab.

4. On the **Microsoft Intune admin center** page, select **Apps**.

    ![](media/media/image1.png)

5. On the **Apps | Overview** blade, under **Manage apps**, select **Protection**.

    ![](media/media/image2.png)

6. In the details pane, select **+ Create policy** and then select **iOS/iPadOS**.

    ![](media/media/image3.png)

7. On the **Basics** tab, configure the following options and select **Next**:

    - Name: **Outlook – Developers**
    - Description: **Policy to prevent cut/copy and paste from Outlook**

    ![](media/media/image4.png)

8. On the **Apps** tab, click **+ Select public apps**.

9. On the **Select apps to target** blade, in the text box, type **Outlook**. Select **Microsoft Outlook**, click the **Select** button, and then select **Next**.

    ![](media/media/image5.png)

    ![](media/media/image6.png)

10. On the **Data protection** tab, configure the following options and select **Next**:

    - Backup Org data to iTunes and iCloud backups: **Block**
    - Send Org data to other apps: **Policy managed apps**
    - Receive data from other apps: **Policy managed apps**
    - Restrict cut, copy, and paste between other apps: **Policy managed apps**

    Leave all other settings at their defaults.

    ![](media/media/image7.png)

11. On the **Access requirements** tab, configure the following options and select **Next**:

    - PIN for access: **Not required**
    - Work or school account credentials for access: **Require**

    ![](media/media/image8.png)

12. On the **Conditional launch** tab, review the settings. Select **Next**.

    ![](media/media/image9.png)

    > **Note:** Here you can set the sign-in security requirements for your app protection policy. You can select a setting and enter the value that users must meet to sign in to your company app. Make note of the various settings but do not change anything.

13. On the **Assignments** tab, under **Included groups**, select **+ Add groups**. Select **Contoso MAM Users**, choose **Select**, and then select **Next**.

    ![](media/media/image10.png)

    > **Note:** An app protection policy with no assignment applies to no one. If you did not complete Lab 10, first create a **Security** group named **Contoso MAM Users** with **Assigned** membership and add **Cindy White** to it (**Groups → New group**), then return to this step.

14. On the **Review + create** tab, review the settings and select **Create**.

    ![](media/media/image11.png)

15. On the **Apps | Protection** blade, in the details pane, verify that **Outlook – Developers** is listed and that its **Deployed** column shows **Yes**.

    ![](media/media/image12.png)

### Task 2: Verify the policy assignment

1. In the **Apps | Protection** blade, select **Outlook – Developers**.

2. On the policy **Overview** page, review the **Properties** and confirm that:

    - **Apps** lists **Microsoft Outlook**
    - **Assignments** includes **Contoso MAM Users**

3. Close Microsoft Edge.

### Task 3 (optional): Test the policy on an iOS/iPadOS device

Complete this task only if you have an iPhone or iPad available.

1. On the iOS/iPadOS device, open **Microsoft Outlook** and sign in as **Cindy@M365xXXXXXXX.onmicrosoft.com** (substitute **XXXXXXX** with your tenant name) with the password **P@55w.rd1234**.

2. When the message **Your organization is now protecting its data in this app** appears, select **OK**. If prompted, close Outlook and open it again.

3. Open an email, copy some text, and try to paste it into a personal app such as **Notes**.

    Notice that the paste is blocked because only policy managed apps can receive Outlook data.

4. On **SEA-SVR1**, in the Intune admin center, select **Apps → Monitor → App protection status** and confirm that Cindy is listed with the **Outlook – Developers** policy for iOS/iPadOS.

**Results**: After completing this exercise, you will have successfully configured and assigned an App protection policy for iOS/iPadOS devices.
