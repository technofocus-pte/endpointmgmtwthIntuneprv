# Lab 2 - Manage Microsoft Entra Device registration

### Summary

In this lab, we will perform Microsoft Entra registration using a Windows device.

## Exercise 1: Configuring Microsoft Entra device registration

### Scenario

Several users have asked to use their personal iOS, Android, and Windows devices to access Contoso cloud resources. Since Contoso does not own the devices, you do not want to have the users perform an Entra join for full device management. Instead, you need to ensure that users are able to register their devices with Microsoft Entra, which still allows you to apply company policy to apps as needed, and still permit users to access Contoso resources. You will test out Microsoft Entra device registration using a Windows 11 device.

### Task 1: Configure Microsoft Entra device registration

1. On **SEA-SVR1**, open a new tab in the Edge browser, enter the URL **https://entra.microsoft.com**, and then press **Enter**.

2. In the **Microsoft Entra admin center** window, navigate and click on **Entra ID**.

    ![](media/media/image1.png)

3. Select **Devices**, then **Device settings**. In the details pane, verify that **Users may register their devices with Microsoft Entra** is set to **All** and is greyed out.

    > **Note:** This option is greyed out and set to **All** by default when Microsoft Intune is enabled in the tenant. This ensures that all users are able to register Windows 10 or newer personal, iOS, Android, and macOS devices with Entra ID.

    ![](media/media/image2.png)

### Task 2: Perform Microsoft Entra registration

1. Switch to **SEA-WS1** and sign in as **Admin** with the password **Pa55w.rd**.

    ![](media/media/image3.png)

2. On the taskbar, select **Start** and then select **Settings**.

    ![](media/media/image4.png)

3. In the **Settings** window, select **Accounts**.

    ![](media/media/image5.png)

4. On the **Accounts** page, select **Access work or school**.

    ![](media/media/image6.png)

5. On the **Access work or school** page, select **Connect**.

    ![](media/media/image7.png)

6. On the **Sign in** page, type **JoniS@M365xXXXXXXXX.onmicrosoft.com** and then select **Next**.

    ![](media/media/image8.png)

7. On the **Enter password** page, enter the tenant password **P@55w.rd1234** and then select **Sign in**.

    ![](media/media/image9.png)

8. On the **You're all set!** page, select **Done**.

    ![](media/media/image10.png)

9. On the **Access work or school** page, verify that Joni's **Work or school account** is displayed.

    ![](media/media/image11.png)

10. Close the **Settings** page.

### Task 3: Validate Microsoft Entra registration

1. On **SEA-WS1**, right-click the **Start** button, and then select **Windows Terminal (Admin)**.

    ![](media/media/image12.png)

2. In the **User Account Control** dialog box, select **Yes**.

    ![](media/media/image13.png)

3. In the PowerShell console, type the following command and press **Enter**:

    ```powershell
    dsregcmd /status
    ```

4. In the output under **User State**, verify that **WorkplaceJoined : YES** is displayed. This indicates that the user has performed a device registration in Microsoft Entra.

    ![](media/media/image14.png)

5. Close PowerShell and then sign out of **SEA-WS1**.

6. Switch to **SEA-SVR1**. In the **Microsoft Entra admin center** window, navigate and click on **Entra ID**.

    ![](media/media/image15.png)

7. Under the **Entra ID** section, select **Devices**, then navigate and click on **All devices** as shown in the below image.

    ![](media/media/image16.png)

8. Verify that the **Join Type** is listed as **Microsoft Entra registered** and that the owner is **Joni Sherman**.

    ![](media/media/image17.png)

    > **Note:** The device is Microsoft Entra registered, NOT Microsoft Entra joined. Entra registered devices are typically devices that cannot be Entra joined, or devices that are personally owned by the user. Registering a device provides access to cloud-based resources.

9. Close Microsoft Edge.

### Task 4: Sign in to Windows and disconnect from the organization

1. Switch to **SEA-WS1**. On the taskbar, select the **Windows Start** icon and then select **Settings**.

    ![](media/media/image4.png)

2. In the **Settings** window, select **Accounts**.

    ![](media/media/image5.png)

3. On the **Accounts** page, select **Access work or school**.

    ![](media/media/image6.png)

4. On the **Access work or school** page, click the dropdown beside the **JoniS@M365xXXXXXXXX** **Work or school** account as shown in the below image.

    ![](media/media/image18.png)

5. Click the **Disconnect** button.

    ![](media/media/image19.png)

6. Click **Yes** to confirm the removal of the account.

    ![](media/media/image20.png)

    > **Note:** You do not have to restart to disconnect a Microsoft Entra registered device.

7. Sign out of **SEA-WS1**.

    ![](media/media/image21.png)

**Results**: After completing this exercise, you will have configured Microsoft Entra device registration.
