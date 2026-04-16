# Lab 2 - Manage Microsoft Entra Device registration.

**Summary**

In this lab, we will perform Microsoft Entra registration using a
Windows device.

**Exercise 1: Configuring Microsoft Entra device registration**

**Scenario**

Several users have asked to use their personal iOS, Android, and Windows
devices to access Contoso cloud resources. Since Contoso does not own
the devices, you do not want to have the users perform an Entra join for
full device management. Instead, you need to ensure that users are able
to register their devices with Microsoft Entra, which still allows you
to apply company policy to apps as needed, and still permit users to
access Contoso resources. You will test out Microsoft Entra device
registration using a Windows 11 device.

**Task 1: Configure Microsoft Entra device registration**

1.  On the
    [*SEA-SVR1*](https://labclient.labondemand.com/Instructions/e7cc4ae1-e3d9-4c55-accc-696f537e1e17?rc=10),
    open a new tab in the Edge browser and enter the following URL,
    !!**https://entra.microsoft.com**!!, then press the **Enter**
    button.

2.  In the **Microsoft Entra admin center** window, navigate and click
    on **Entra** **Id**.

![](media/media/image1.png)

3.  Select **Devices**, then **Device settings** page, in the details
    pane, verify that **Users may register their devices with Microsoft
    Entra** is set to **All** and is greyed out.

> This option is greyed out and set to **All** by default when Microsoft
> Intune is enabled in the tenant. This ensures that all users are able
> to register Windows 10 or newer personal, iOS, Android, and macOS
> devices with Entra ID.
>
> ![](media/media/image2.png)

**Task 2: Perform Microsoft Entra registration**

1.  Switch
    to [*SEA-WS1*](https://labclient.labondemand.com/Instructions/e7cc4ae1-e3d9-4c55-accc-696f537e1e17?rc=10) and
    sign in as **Admin** with the password of !!**Pa55w.rd**!!.

![A screenshot of a computer Description automatically generated with
medium confidence](media/media/image3.png)

2.  On the taskbar, select **Start** and then select **Settings**.

![A screenshot of a computer Description automatically
generated](media/media/image4.png)

3.  In the **Settings** window, select **Accounts**.

![A screenshot of a computer Description automatically
generated](media/media/image5.png)

4.  On the **Accounts** page, select **Access work or school**.

![A screenshot of a computer Description automatically
generated](media/media/image6.png)

5.  In the **Access work or school** page, select **Connect**.

![A screenshot of a computer Description automatically
generated](media/media/image7.png)

6.  On the **Sign in** page,
    type !!**JoniS@M365xXXXXXXX.onmicrosoft.com**!!  and then
    select **Next**.

![](media/media/image8.png)

7.  On the **Enter password** page, enter the tenant password:
    !\![**P@55w.rd1234**](mailto:P@55w.rd1234)!! and then select **Sign
    in**

![A screenshot of a computer Description automatically
generated](media/media/image9.png)

8.  On the **You're all set!** page, select **Done**.

![A screenshot of a computer Description automatically
generated](media/media/image10.png)

9.  On the **Access work or school** page, verify that Joni's **Work or
    school account** is displayed.

![A screenshot of a computer Description automatically
generated](media/media/image11.png)

10. Close the **Settings** page.

**Task 3: Validate Microsoft Entra registration**

1.  On [*SEA-WS1*](https://labclient.labondemand.com/Instructions/e7cc4ae1-e3d9-4c55-accc-696f537e1e17?rc=10),
    right-click on **Start button**, and then select **Windows Terminal
    (Admin)**.

> ![A screenshot of a computer Description automatically
> generated](media/media/image12.png)

2.  On the **User Account Control** dialog box, select **Yes**.

> ![A screenshot of a computer error Description automatically
> generated](media/media/image13.png)

3.  In the PowerShell console, type the following and press **Enter**:

> !!**dsregcmd /status**!!

4.  In the output under **User State**, verify that **WorkplaceJoined :
    YES** is displayed. This indicates that the user has performed a
    device registration in Microsoft Entra.

> ![A screenshot of a computer Description automatically
> generated](media/media/image14.png)

5.  Close PowerShell and then sign out of **SEA-WS1**.

6.  Switch to SEA-SVR1. Go to **Microsoft Entra admin center** window,
    navigate and click on **Entra Id**.

> ![](media/media/image15.png)
>
> 7\. Under the **Entra** **Id** section, select **Devices**, then
> navigate and click on **All devices** as shown in the below image.
>
> ![](media/media/image16.png)

8.  Verify that the **Join Type** is listed as **Microsoft Entra
    registered** and that the owner is **Joni Sherman**.

> ![](media/media/image17.png)
>
> Notice that the device is Microsoft Entra registered, NOT Microsoft
> Entra joined. Entra registered devices are typically devices that
> cannot be Entra joined, or devices that are personally owned by the
> user. Registering a device will provide access to Cloud based
> resources.

9.  Close Microsoft Edge.

**Task 4: Sign in to Windows and disconnect from the organization**

1.  Switch
    to *[SEA-WS1](https://labclient.labondemand.com/Instructions/e7cc4ae1-e3d9-4c55-accc-696f537e1e17?rc=10).* On
    the taskbar, select **Windows Start icon** button and then
    select **Settings**.

![A screenshot of a computer Description automatically
generated](media/media/image4.png)

2.  In the **Settings** window, select **Accounts**.

> ![A screenshot of a computer Description automatically
> generated](media/media/image5.png)

3.  On the **Accounts** page, select **Access work or school**.

> ![A screenshot of a computer Description automatically
> generated](media/media/image6.png)

4.  In the **Access work or school** page, click on the dropdown beside
    **JoniS@M3654xXXXXXXXX** **Work or school** account as shown in the
    below image.

> ![](media/media/image18.png)

5.  Click on **Disconnect** button.

> ![A screenshot of a computer Description automatically
> generated](media/media/image19.png)

6.  Click on the **Yes** button to confirm the removal of the account.

> ![A screenshot of a computer Description automatically
> generated](media/media/image20.png)
>
> Notice that you do not have to restart to disconnect a Microsoft Entra
> registered device.

7.  Sign out of **SEA-WS1**.

![A screenshot of a computer Description automatically
generated](media/media/image21.png)

**Results**: After completing this exercise, you will have configured
Microsoft Entra device registration.
