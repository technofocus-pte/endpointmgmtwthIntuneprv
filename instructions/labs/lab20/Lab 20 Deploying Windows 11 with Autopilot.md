# Lab 20: Deploying Windows 11 with Autopilot

**Summary**

In this lab you will learn how provision a Windows 11 device with
Autopilot using User-driven mode.

**Prerequisites**

To following lab(s) must be completed before this lab:

-   Lab 01-Managing Identities in Microsoft Entra ID

-   Lab 02-Synchronizing Identities by using Azure AD Connect

-   Lab 11-Deploying Windows 11 using Microsoft Deployment Toolkit

**Scenario**

Contoso IT is planning to roll out a deployment of new Windows 11
devices using Autopilot. The devices have a default installation of
Windows 11. Users should be able to connect the device, turn it on, and
answer minimal questions during the OOBE, using their Microsoft Entra ID
credentials to sign in. The process should automatically enroll and join
the Entra ID domain. You have been asked to configure and test the
experience using the SEA-WS4, which you recently installed and
configured using Hyper-V.

## Task 1: Create a group in Microsoft Entra Admin center.

1.  Switch and Sign in
    to SEA-SVR1 as !!**Contoso\\Administrator**!! with the
    the password !!Pa55w.rd!! and
    close **Server Manager**.  
 
2.  On the taskbar, select **Microsoft Edge**.

3.  In Microsoft Edge, in the address bar, type !!https://entra.microsoft.com!!, and
    then press **Enter**. If prompted, sign in with your admin credentials.

    ![](./media/image1.png) 

4.  In the navigation pane, select **Identity.**

5.  Under **Identity**, select **Groups**.

    ![](./media/image2.png) 
6.  In the **Groups \| All groups** blade, select **New group**.

    > ![](./media/image3.png) 
 
7.  In the **New Group** blade, in the **Group type** list,
    select **Security**.

8.  In the **Group name** box, type !!IT Devices!!.

9.  In the **Group description** box, type !!IT Department Devices!!.

10. In the **Membership type** list, select **Dynamic Device**.

11. Select **Add dynamic query**.

    > ![](./media/image4.png)

12. On the **Dynamic membership rules** blade select **Edit** above
    the **Rule syntax** box.

    > ![](./media/image5.png)
13. In the Edit rule syntax text box, add the following simple
    membership rule and select **OK**.

14. !!(device.devicePhysicalIDs -any (\_ -contains \"\[ZTDId\]\"))!!

    > ![](./media/image6.png) 

15. Select **Save** to close **Dynamic membership rules**, and then
    select **Create** to create the group.

    > ![A screenshot of a computer Description automatically
    > generated](./media/image7.png) 

    > ![A screenshot of a computer Description automatically
    > generated](./media/image8.png)

    > ![](./media/image9.png) 
 
## Task 2: Generate a device-specific comma-separated value (CSV) file

1.  Switch to SEA-SVR2 and sign in
    as Contoso\\Administrator with the
    password of !!Pa55w.rd!!.

    > ![A screenshot of a computer Description automatically
    > generated](./media/image10.png)

2.  Select **Hyper-V Manager** in the taskbar.

    > ![A screenshot of a computer Description automatically
    > generated](./media/image11.png)

3.  Under Virtual Machines, right-click **SEA-WS4** and
    select **Connect**.

    > ![](./media/image12.png)

4.  On the **SEA-WS4** window, select **Start**. When the computer
    starts, maximize the window.

    > ![A screenshot of a computer Description automatically
    > generated](./media/image13.png) 

5.  Sign in
    to **SEA-WS4** as Administrator with
    the password of  !!Pa55w.rd!!.

    > ![A screenshot of a computer Description automatically
    > generated](./media/image14.png)

6.  Right-click **Start**, select **Windows Terminal (Admin)**, and then
    select **Yes** at the **User Account Control** prompt.

    > ![](./media/image15.png)

    > ![A screenshot of a computer error Description automatically
    > generated](./media/image16.png) 

7.  At the Windows PowerShell command-line prompt, type the following
    cmdlet, and then press **Enter**:

     !!Install-Script -Name Get-WindowsAutoPilotInfo!!

    ![A screenshot of a computer Description automatically
    generated](./media/image17.png) 

8.  You will receive three prompts. Each time,
    type **Y**, and then press **Enter**.

     ![](./media/image18.png) 
 
9.  At the Windows PowerShell command-line prompt, type the following
    cmdlet, and then press **Enter**:

    > !!Set-ExecutionPolicy RemoteSigned!!

10. When prompted, type !!Y!!, and then
    press Enter.

11. At the Windows PowerShell command-line prompt, type the following
    cmdlet, and then press **Enter**:

    > !!Get-WindowsAutoPilotInfo.ps1 -OutputFile C:\\Computer.csv!!
    
    > ![](./media/image19.png)
12. At the Windows PowerShell command-line prompt, type the following
    command, press **Enter**, and then review the file content:

13. **type** !!C:\\Computer.csv!!

     ![](./media/image20.png) 
 
14. At the Windows PowerShell command-line prompt, type the following
    command, press **Enter**. This will copy the file to **SEA-SVR2**:

15. copy !!c:\\computer.csv \\\\sea-svr2\\labfiles!!

    > ![A screenshot of a computer screen Description automatically
    > generated](./media/image21.png)

16. Close the Windows PowerShell command prompt.

Task 3: Work with a Windows Autopilot deployment profile

1.  Switch to SEA-SVR1
    > ![](./media/image22.png)
2.  In **Microsoft Edge**, open a new tab and navigate to https://intune.microsoft.com
    If prompted, sign in with admin@M365xXXXXXXX.onmicrosoft.com and password given in the resources tab.

3.  In the **Microsoft Intune admin center**, select **Devices**.

4.  In the **Device enrollment** section, select **Enroll devices**.

5.  In the details pane scroll down to **Windows Autopilot Deployment
    Program**, and then select **Devices**.

    > ![A screenshot of a computer Description automatically
    > generated](./media/image23.png)

6.  In the **Windows Autopilot devices** blade on the menu bar,
    select **Import**, select the **folder icon** and then browse
    to !!\\SEA-SVR2\\Labfiles!!,
    select **Computer.csv**, select **Open**, and then
    select **Import**.

    > ![](./media/image24.png)
    > ![A screenshot of a computer Description automatically
    > generated](./media/image25.png)

    > ![A screenshot of a computer Description automatically
    > generated](./media/image26.png)
    > ![A screenshot of a computer Description automatically
    > generated](./media/image27.png)

    > **Note**: The import process can take up to 15 minutes, but normally
    > takes around 5 minutes.
    >
    > **Important**: After the process is complete, the device may not show.
    > If this is the case, select the **Sync** button, wait a few minutes,
    > and then select **Refresh**.

7.  Select **X** to close the **Windows Autopilot devices** blade.

    > ![](./media/image28.png)

8.  On the Windows enrollment blade, in the details pane,
    select **Deployment Profiles**.

    > ![](./media/image29.png)
 
9.  On the **Windows AutoPilot deployment profiles** blade,
    select **Create profile** and then select **Windows PC**.

    > ![](./media/image30.png)
 
10. In the **Basics** tab, in the **Name** text box, type !!Contoso profile1!!.

11. For **Convert all targeted devices to Autopilot** select **No**, and
    then select **Next**.

    > ![A screenshot of a computer Description automatically
    > generated](./media/image31.png)
12. On the **Out-of-box experience (OOBE)** tab, ensure that
    the **Deployment mode** is set to **User-Driven**.

13. Ensure that **Join to Microsoft Entra ID as** is set to **Microsoft
    Entra Joined**.

14. Ensure that the following options are set:

    -   Microsoft Software License Terms: **Hide**

    -   Privacy Settings: **Hide**

    -   Hide change account options: **Hide**

    -   User account type: **Administrator**.

    -   Allow pre-provisioned deployment: **No**

    -   Language (Region): **Operating system default**

    -   Automatically configure keyboard: **Yes**

    -   Apply device name template: **No**

15. Select **Next**.

    > ![](./media/image32.png)
16. On the **Assignments** tab, under **Included groups** select **Add
    groups**.

17. Select the **IT Devices** group and click **Select**.
    Select **Next**.

    > ![](./media/image33.png)
    >
    > ![A screenshot of a computer Description automatically
    > generated](./media/image34.png)cription automatically
    > generated](./media/image35.png)
18. On the **Review + create** blade, review the information and then
    select **Create**.

    > ![A screenshot of a computer Description automatically
    > generated](./media/image36.png)
    >
    > ![](./media/image37.png)
 
## Task 4: Reset the PC

1.  Switch to SEA-SVR2.
    The **SEA-WS4** computer should be still maximized.

    > ![](./media/image38.png)
 
2.  On **SEA-WS4**, select **Start**, type !!"**reset**!!  and select **Reset
    this PC**.

    > ![](./media/image39.png)

3.  In the **Reset this PC** section, select **Reset PC**.

    > ![A screenshot of a computer Description automatically
    > generated](./media/image40.png)

4.  Select **Remove everything**, and then select **Local reinstall**.

    > ![A blue screen with white text Description automatically
    > generated](./media/image41.png)
    >
    > ![A blue screen with white text Description automatically
    > generated](./media/image42.png)

5.  Select **Next** and then select **Reset**.

    > ![A screenshot of a computer Description automatically
    > generated](./media/image43.png)
    >
    > ![A blue screen with white text Description automatically
    > generated](./media/image44.png)
    > **Note**: Normally this task is not required for new deployment of
    > physical devices. The device's autopilot info is either provided by
    > the manufacturer or can be obtained from the device prior to the OOBE.
    > For the purposes of this lab, we must initiate a reset to simulate a
    > new device OOBE.
    >
    > **Note**: This process can take 45-60 minutes and will reboot several
    > times during the process. Your instructor may continue with the next
    > module while this task completes. Be sure to come back to complete
    > Task 5 during your next lab session.

## Task 5: Verify Autopilot deployment

1.  At the **Contoso Corp. Sign-in Page**, enter  !!Cindy@M365x19242953.onmicrosoft.com!! and
    select **Next**.

2.  At the Password page, enter !!P@55w.rd1234!! and select **Sign in**.

3.  At the **Use Windows Hello with your account**, select **OK**.

    > ![A screenshot of a computer Description automatically
    > generated](./media/image45.png)

4.  At the **Verify your identity** page, select the Text verification
    method.

    > ![A screenshot of a computer Description automatically
    > generated](./media/image46.png)

5.  At the **Enter code** page, enter the code that has been texted to
    your mobile device and then select **Verify**.

    > ![A screenshot of a computer Description automatically
    > generated](./media/image47.png)

6.  On the **Setup up a PIN** dialog box, in the **New
    PIN** and **Confirm PIN** fields,
    enter 102938, and then
    select **OK**.

    > ![A screenshot of a computer Description automatically
    > generated](./media/image48.png)
7.  On the **All set!** page, select **OK**.

8.  Select **Start** and select **Settings**.

    > ![A screenshot of a computer Description automatically
    > generated](./media/image49.png)

9.  Select **Accounts**, and then select **Access work or school**.
    Verify the device is connected to Contoso\'s Azure AD.

    > ![A screenshot of a computer Description automatically
    > generated](./media/image50.png)

10. Select **Connected to Contoso\'s Azure AD** and select **Info**.

    > ![A screenshot of a computer Description automatically
    > generated](./media/image51.png)

11. On the **Managed by Contoso** page, scroll down and then
    select **Sync**.

    > ![A screenshot of a computer Description automatically
    > generated](./media/image52.png)
    > ![](./media/image53.png)
12. On **SEA-WS4**, close the **Settings** window.

13. Switch to SEA-SVR1.

14. In the Microsoft Entra admin center, select **Identity**,
    select **Devices** and then select **All devices**.

    > ![](./media/image54.png)
    > Note that the new device displays with a name beginning with
    > \"**DESKTOP-**\". Also note that the Join Type is **Microsoft Entra ID
    > joined** with Cindy White as the owner.

15. Select the Autopilot device. Review the management options along the
    top menu bar.

> Notice that you can **Retire, Wipe, Sync,** and **Restart** the
> device.

16. Select the ellipse at the end of the menu bar and take notice of the
    additional management capabilities.

    > ![A screenshot of a computer Description automatically
    > generated](./media/image55.png) 
    >
    > ![A screenshot of a computer Description automatically
    > generated](./media/image56.png) 
    >
    > Additional capabilities include Fresh Start, Autopilot Reset, Quick
    > scan, Full scan, as well as others.

17. Close Microsoft Edge.

**Results**: After completing this exercise, you will have provisioned a
Windows 11 device with Autopilot using User-driven mode.
