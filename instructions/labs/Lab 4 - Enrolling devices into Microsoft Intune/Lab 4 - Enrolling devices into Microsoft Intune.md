# Lab 4 - Enrolling devices into Microsoft Intune

### Summary

In this lab, you will join a Windows client to Entra ID and verify that the device has automatically enrolled into Microsoft Intune.

### Prerequisites

The following lab(s) must be completed before this lab:

- Lab #1-Managing Identities in Microsoft Entra ID
- Lab #3-Manage Device Enrollment into Microsoft Intune

> **Note:** You may also need a mobile phone that can receive text messages used to secure Windows Hello sign-in authentication to Entra ID.

### Scenario

You have assigned Cindy White appropriate licenses and will now test the process of joining a Windows device to Entra ID and have it automatically enroll in Microsoft Intune.

### Task 1: Automatically enroll a Windows device to Microsoft Intune

1. Switch to **SEA-WS1** and sign in as **Admin** with the password **Pa55w.rd**.

    ![](media/media/image1.png)

2. On the taskbar, select **Start** and then select **Settings**.

    ![](media/media/image2.png)

3. In the **Settings** window, select **Accounts**.

    ![](media/media/image3.png)

4. On the **Accounts** page, select **Access work or school**.

    ![](media/media/image4.png)

5. On the **Access work or school** page, select **Connect**.

    ![](media/media/image5.png)

6. In the **Microsoft account** window, select **Join this device to Microsoft Entra ID**.

    ![](media/media/image6.png)

7. On the **Sign in** page, type **Cindy@M365xXXXXXXX.onmicrosoft.com** (substitute **XXXXXXX** with your tenant name) and then select **Next**.

    ![](media/media/image7.png)

8. On the **Enter password** page, enter the password **P@55w.rd1234** and then select **Sign in**.

    ![](media/media/image8.png)

9. When the **Make sure this is your organization** dialog box appears, select **Join**.

    ![](media/media/image9.png)

10. On the **You're all set!** page, read the information and then select **Done**.

    ![](media/media/image10.png)

11. In the **Access work or school** section, verify that **Connected to Contoso's Azure AD** displays.

12. Select **Connected to Contoso's Azure AD** and then select **Info**.

    ![](media/media/image11.png)

13. Take note of the information regarding the areas managed by Contoso, scroll down, and then select **Sync**. This will force a device sync with Intune.

    ![](media/media/image12.png)

14. Close the **Settings** window.

### Task 2: Validate device enrollment into Microsoft Entra and Intune

1. On the **SEA-WS1** taskbar, select **Start**, type **certlm.msc** and press **Enter**.

    ![](media/media/image13.png)

2. In the **User Account Control** dialog box, select **Yes**.

    ![](media/media/image14.png)

3. In the **Certificates** console, in the navigation pane, expand **Personal** and select the **Certificates** node. Verify that the following certificates are listed in the details pane:

    - Microsoft Intune MDM Device CA
    - MS-Organization-Access
    - MS-Organization-P2P-Access [2024]

    This indicates that the device is enrolled in Microsoft Entra and Intune.

    ![](media/media/image15.png)

4. Close the **Certificates** window.

5. Right-click the **Start** button and then select **Windows Terminal (Admin)**.

    ![](media/media/image16.png)

6. In the **User Account Control** dialog box, select **Yes**.

    ![](media/media/image17.png)

7. In the PowerShell console, type the following command and press **Enter**:

    ```powershell
    dsregcmd /status
    ```

8. In the output, under **Device State**, verify that **AzureAdJoined : YES** is displayed. This indicates that the device is Microsoft Entra joined.

    ![](media/media/image18.png)

9. In the output under **Tenant Details**, verify that the following three entries exist:

    - **MdmUrl**: https://enrollment.manage.microsoft.com/enrollmentserver/discovery.svc
    - **MdmTouUrl**: https://portal.manage.microsoft.com/TermsofUse.aspx
    - **MdmComplianceUrl**: https://portal.manage.microsoft.com/?portalAction=Compliance

    ![](media/media/image19.png)

    > **Note:** These entries indicate that the device is enrolled in Intune.

### Task 3: Sign in as Microsoft Entra ID user

1. Sign out of **SEA-WS1**, as you are logged in with the local admin account.

2. On the sign-in screen, select **Other user** and sign in as **Cindy@M365xXXXXXXX.onmicrosoft.com** with the password **P@55w.rd1234**.

    ![](media/media/image20.png)

3. Wait for the profile to be created.

    ![](media/media/image21.png)

    > **Note:** If you are prompted for **Windows Hello**, complete the sign-in process accordingly. On the **Set up a PIN** page, in the **New PIN** and **Confirm PIN** boxes, type **102938** and then select **OK**.

    ![](media/media/image22.png)

4. Sign out of **SEA-WS1**.

### Task 4: Verifying device enrollment in the Microsoft Intune console

1. Switch to **SEA-SVR1** and sign in using the provided credentials.

2. In the Microsoft Edge browser, type **https://intune.microsoft.com** in the address bar, and then press **Enter**. Sign in with your Office 365 Tenant administrator account.

3. In the navigation pane, select **Devices**.

    ![](media/media/image23.png)

4. On the **Devices | Overview** page, navigate and click on **Windows**.

    ![](media/media/image24.png)

5. Navigate and click on **Windows devices**. Verify that **SEA-WS1** is listed.

    Note that for SEA-WS1, the **Managed by** column displays **Intune** and the **Ownership** column displays **Corporate**.

    ![](media/media/image25.png)

    > **Note:** This view lists devices that are enrolled in Intune. Remember that you configured automatic enrollment between Microsoft Entra and Microsoft Intune, and because of that, any device that is joined or registered to Microsoft Entra is automatically enrolled in Microsoft Intune. Any devices joined prior to setting up enrollment are only joined or registered to Entra, but not enrolled in Intune.

6. Open a new tab and navigate to the **Microsoft Entra admin center** at **https://entra.microsoft.com**. Click on **Devices** and then select **All devices**.

    ![](media/media/image26.png)

    ![](media/media/image27.png)

7. Take note of **SEA-WS1**. Notice that the **Join Type** column displays **Microsoft Entra joined** and the **MDM** column displays **Microsoft Intune**.

    ![](media/media/image28.png)

**Results**: After completing this exercise, you will have successfully joined a Windows client to Microsoft Entra ID and verified that the device has automatically enrolled into Microsoft Intune.
