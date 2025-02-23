    Lab 03: Configuring and managing Microsoft Entra ID Join

**Summary**

In this lab, you will configure Microsoft Entra ID Join settings and
perform both standard and Microsoft Entra hybrid join scenarios for
Windows devices.

**Prerequisites**

To following lab(s) must be completed before this lab:

- Lab \#2: Synchronizing Identities by using Microsoft Entra Connect

**Note**: You will also need a mobile phone that can receive text
messages used to secure Windows Hello sign in authentication to Entra
ID.

**Exercise 1: Configuring Microsoft Entra Join**

**Scenario**

You need to configure Entra ID device settings to ensure that all users
are allowed to join devices to Entra ID. You also need to ensure that
users can only join a maximum of 20 devices and that Allan Deyoung is
added as a local administrator on all Microsoft Entra Joined devices.
Finally, you will verify that Microsoft Entra Join works as expected by
having Joni Sherman join SEA-WS1 to the tenant.

## Task 0: Enable TLS 1.2 using PowerShell script.

1.  On SEA-WS1, sign in as Contoso\Administrator with the password of
    Pa55w.rd

2.  On the start menu
    type [**PowerShell**](urn:gd:lg:a:send-vm-keys) right click on
    PowerShell and select run as administrator.

    ![](./media/image1.png)

3.  Run the following script on the PowerShell.

**If** (-Not (Test-Path
'HKLM:\SOFTWARE\WOW6432Node\Microsoft\\NETFramework\v4.0.30319'))

{

New-Item 'HKLM:\SOFTWARE\WOW6432Node\Microsoft\\NETFramework\v4.0.30319'
-Force | Out-Null

}

New-ItemProperty -Path
'HKLM:\SOFTWARE\WOW6432Node\Microsoft\\NETFramework\v4.0.30319' -Name
'SystemDefaultTlsVersions' -Value '1' -PropertyType 'DWord' -Force |
Out-Null

New-ItemProperty -Path
'HKLM:\SOFTWARE\WOW6432Node\Microsoft\\NETFramework\v4.0.30319' -Name
'SchUseStrongCrypto' -Value '1' -PropertyType 'DWord' -Force | Out-Null

**If** (-Not (Test-Path
'HKLM:\SOFTWARE\Microsoft\\NETFramework\v4.0.30319'))

{

New-Item 'HKLM:\SOFTWARE\Microsoft\\NETFramework\v4.0.30319' -Force |
Out-Null

}

New-ItemProperty -Path
'HKLM:\SOFTWARE\Microsoft\\NETFramework\v4.0.30319' -Name
'SystemDefaultTlsVersions' -Value '1' -PropertyType 'DWord' -Force |
Out-Null

New-ItemProperty -Path
'HKLM:\SOFTWARE\Microsoft\\NETFramework\v4.0.30319' -Name
'SchUseStrongCrypto' -Value '1' -PropertyType 'DWord' -Force | Out-Null
```
**If** (-Not (Test-Path
'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS
1.2\Server'))

{

New-Item
'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS
1.2\Server' -Force | Out-Null

}

New-ItemProperty -Path
'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS
1.2\Server' -Name 'Enabled' -Value '1' -PropertyType 'DWord' -Force |
Out-Null

New-ItemProperty -Path
'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS
1.2\Server' -Name 'DisabledByDefault' -Value '0' -PropertyType 'DWord'
-Force | Out-Null

**If** (-Not (Test-Path
'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS
1.2\Client'))

{

New-Item
'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS
1.2\Client' -Force | Out-Null

}

New-ItemProperty -Path
'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS
1.2\Client' -Name 'Enabled' -Value '1' -PropertyType 'DWord' -Force |
Out-Null

New-ItemProperty -Path
'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS
1.2\Client' -Name 'DisabledByDefault' -Value '0' -PropertyType 'DWord'
-Force | Out-Null

Write-Host 'TLS 1.2 has been enabled. You must restart the Windows
Server for the changes to take affect.' -ForegroundColor Cyan
```

![](./media/image2.png)

4.  Restart the Windows Server VM.

![](./media/image3.png)

## Task 1: Configure Microsoft Entra ID join Device settings

1.  Switch to **SEA-SVR1**. In the **Microsoft Edge** browser address
    bar, type the following URL:
    !\![**https://entra.microsoft.com**](https://entra.microsoft.com)!!
    and press the **Enter** button.

2.  Sign in with your O365 tenant ID:
    !!**admin@M365xXXXXXXXX.onmicrosoft.com**!!, and use the tenant
    Admin password.

![A screenshot of a computer Description automatically
generated](./media/image4.png)

![A screenshot of a login box Description automatically
generated](./media/image5.png)

3.  On **Stay signed in?** dialog box, select the **Yes** button.

![A screenshot of a computer Description automatically
generated](./media/image6.png)

4.  In the **Microsoft Entra admin center** window, navigate and click
    on **Identity**.

![A screenshot of a computer Description automatically
generated](./media/image7.png)

5.  Under the **Identity** section, select **Devices**, then navigate
    and click on **All devices** as shown in the below image.

![A screenshot of a computer Description automatically
generated](./media/image8.png)

Notice that there are no devices found, as you have not joined any
devices yet.

![](./media/image9.png)

6.  On the **Devices** | All devices page, select **Device settings**.

![A screenshot of a computer Description automatically
generated](./media/image10.png)

7.  On the **Devices | Device settings** page, in the details pane,
    under **Users may join devices to Entra**, verify that **All** is
    selected.

This indicates that all Entra users are permitted to join Windows 10 or
newer devices to Microsoft Entra. Note that this setting does not apply
to Entra hybrid joined devices, or devices joined by using Windows
Autopilot self-deployment mode.

8.  In the **Require Multi-factor Authentication to register or join
    devices with Entra** section, verify that the setting is set
    to **No**.

![A screenshot of a computer Description automatically
generated](./media/image11.png)

9.  In the **Maximum number of devices per user** section, select **20
    (Recommended)**.

10. Click on **Manage** **Additional local administrators on all
    Microsoft Entra Joined devices** link. The **Device Administrators
    page** opens.

![A screenshot of a computer Description automatically
generated](./media/image12.png)

11. In the **Device Administrators | Assignments** page, select **Add
    assignments**.

![A screenshot of a computer Description automatically
generated](./media/image13.png)

12. In the Search box, enter !!**Allan Deyoung**!!, select the **Allan
    Deyoung** user object, and then select **Add**.

![A screenshot of a computer Description automatically
generated](./media/image14.png)

13. Allan Deyoung will now be added as a Device Administrator on all
    Microsoft Entra Joined devices.

![A screenshot of a computer screen Description automatically
generated](./media/image15.png)

14. Click on **Devices | Device settings** link below Azure portal
    search bar to go back to **Device Settings** page.

![A screenshot of a computer Description automatically
generated](./media/image16.png)

15. On the **Device settings** page, select **Save**.

![A screenshot of a computer Description automatically
generated](./media/image17.png)

**Task 2: Perform Microsoft Entra ID Join**

1.  Switch
    to [SEA-WS1](https://labclient.labondemand.com/Instructions/e7cc4ae1-e3d9-4c55-accc-696f537e1e17?rc=10) and
    sign in as **Admin** with the password of !!**Pa55w.rd**!!.

![](./media/image18.png)

2.  On the taskbar, select **Windows Start button** icon and then
    select **Settings**.

![](./media/image19.png)

3.  In the **Settings** window, select **Accounts**.

![A screenshot of a computer Description automatically
generated](./media/image20.png)

4.  On the **Accounts** page, select **Access work or school**.

![A screenshot of a computer Description automatically
generated](./media/image21.png)

5.  In the **Access work or school** page, select **Connect**.

![A screenshot of a computer Description automatically
generated](./media/image22.png)

6.  In the **Microsoft account** window, select **Join this device to
    Microsoft Entra ID**.

![A screenshot of a computer screen Description automatically
generated](./media/image23.png)

7.  On the **Sign in** page, type 
    !!JoniS@M365xXXXXXXX.onmicrosoft.com!!  and then select **Next**.

![Graphical user interface, application, Teams Description automatically
generated](./media/image24.png)

8.  On the **Enter password** page, enter the tenant password:
    !\![**P@55w.rd1234**](mailto:P@55w.rd1234)!! and then select **Sign
    in**.

![Graphical user interface, application Description automatically
generated](./media/image25.png)

9.  On the **Make sure this is your organization** dialog box,
    select **Join**.

![A screenshot of a computer error Description automatically
generated](./media/image26.png)

10. On the **You're all set!** page, select **Done**.

![A screenshot of a computer Description automatically
generated](./media/image27.png)

11. On the **Access work or school** page, verify that **Connected to
    Contoso's Azure AD** is displayed.

![A screenshot of a computer Description automatically
generated](./media/image28.png)

12. Close the **Settings** page.

**Task 3: Validate Microsoft Entra Join**

1.  On [SEA-WS1](https://labclient.labondemand.com/Instructions/e7cc4ae1-e3d9-4c55-accc-696f537e1e17?rc=10),
    right-click on **Windows** **Start button** icon, and then
    select **Windows Terminal (Admin)** as shown in the below image.

![](./media/image29.png)

2.  On **User Account Control** dialog box, select **Yes**.

![](./media/image30.png)

3.  In the PowerShell console, type the following command and press the
    **Enter** button:

!!**dsregcmd /status**!!

4.  In the output, under **Device State**, verify that **AzureAdJoined :
    YES** is displayed.

This indicates that the device is Microsoft Entra Joined.

![](./media/image31.png)

5.  Close PowerShell.

6.  Right-click again on **Windows** **Start** **button** icon and then
    select **Computer Management**.

![A screenshot of a computer Description automatically
generated](./media/image32.png)

7.  In **Computer Management** window, expand **Local Users and
    Groups**, and then select **Groups**.

![](./media/image33.png)

![A screenshot of a computer Description automatically
generated](./media/image34.png)

8.  Double-click the **Administrators** group.

![A screenshot of a computer Description automatically
generated](./media/image35.png)

Notice that Joni Sherman has been added as a local Administrator
On [SEA-WS1](https://labclient.labondemand.com/Instructions/e7cc4ae1-e3d9-4c55-accc-696f537e1e17?rc=10).
Also notice two security principals represented by their security
identifiers (SID). These two SIDs represent the Entra global
administrator role and the Microsoft Entra Joined device administrator
role.

![](./media/image36.png)

9.  Close all open windows and sign out of SEA-WS1 by clicking on
    **Windows Start button icon \> Admin \> Sign out**.

![](./media/image37.png)

10. Switch to **SEA-SVR1** and login with the credentials
    **Contoso\Administrator** and password !!**Pa55w.rd**!!

![A screenshot of a computer Description automatically
generated](./media/image38.png)

11. In **Microsoft Entra admin center**, navigate and click on
    **Identity**.

12. Navigate and select **Devices**, then click on **All devices**.

13. In the **Devices | All devices** page, notice that **SEA-WS1** is
    listed.

![](./media/image39.png)

14. Verify that the **Join Type** is listed as **Microsoft Entra
    Joined** and that the owner is **Joni Sherman**.

![](./media/image40.png)

15. Also note that the MDM column shows **None**. This indicates that
    this device is not yet managed by Microsoft Intune.

![A screenshot of a computer Description automatically
generated](./media/image41.png)

**Task 4: Sign in to Windows as Microsoft Entra User**

1.  Switch to **SEA-WS1** and click on **Other user.**

![](./media/image42.png)

2.  **Sign** in as !!**JoniS@M365xXXXXXXX.onmicrosoft.com**!!  with the
    tenant password: !!**P@55w.rd1234**!!

**Note: Wait for the profile to be created.**

![](./media/image43.png)

**Note** – If you are prompted for **Windows Hello**, then complete the
sign in process accordingly and on the **Set up a PIN** page, in
the **New PIN** and **Confirm PIN** boxes, type !!**102938**!!  and then
select **OK**.

![](./media/image44.png)

**Task 5: Remove a Windows device from Entra**

1.  On [SEA-WS1](https://labclient.labondemand.com/Instructions/e7cc4ae1-e3d9-4c55-accc-696f537e1e17?rc=10),
    login with Joni Sherman if prompted and if the option to enter the
    Pin is available then enter the pin: !!**102938**!! or enter the
    password as !!**P@55w.rd1234**!!

![A screenshot of a computer Description automatically
generated](./media/image45.png)

2.  In the **Settings** window, select **Accounts**.

![A screenshot of a computer Description automatically
generated](./media/image46.png)

3.  In the left-sided navigation pane, navigate and click on
    **Accounts**. On the **Accounts** page, select **Access work or
    school**.

![A screenshot of a computer Description automatically
generated](./media/image47.png)

4.  In the **Access work or school** page, select the dropdown beside
    **Connected to Contoso's Azure AD** as shown in the below image.
    Click on **Disconnect** and then select **Yes**.

![](./media/image48.png)

![A screenshot of a computer Description automatically
generated](./media/image49.png)

![A screenshot of a computer Description automatically
generated](./media/image50.png)

5.  On the **Disconnect from the organization** page,
    select **Disconnect**.

![A blue box with white text Description automatically
generated](./media/image51.png)

6.  On the **Windows Security** dialog box, in the **Email
    address** box, enter !!Admin!! and in the **Password** box,
    type !!Pa55w.rd!!. Select **OK**.

![Graphical user interface Description automatically
generated](./media/image52.png)

7.  In the **Restart your PC** dialog box, select **Restart now**.
    **SEA-WS1** restarts.

![A blue box with white text Description automatically
generated](./media/image53.png)

**Results**: After completing this exercise, you will have configured
Microsoft Entra device settings, joined a device to Entra, and removed a
device from Entra.

**Exercise 2: Configuring Microsoft Entra hybrid join**

**Scenario**

Some Contoso Windows devices are currently joined to the local Active
Directory Domain Services. To enable those devices to seamlessly access
cloud services you plan to enable Microsoft Entra hybrid join. You will
test Microsoft Entra hybrid join by re-configuring Azure AD Connect and
testing out the process on SEA-CL2.

**Task 1: Prepare the environment**

1.  Switch
    to [SEA-SVR1](https://labclient.labondemand.com/Instructions/e7cc4ae1-e3d9-4c55-accc-696f537e1e17?rc=10).

![A picture containing text Description automatically
generated](./media/image54.png)

2.  Select **Windows** **Start icon** button, expand **Windows
    Administrative Tools**, and then select **Active Directory Users and
    Computers**.

![](./media/image55.png)

3.  In **Active Directory Users and Computers**,
    right-click **Contoso.com**, point to **New**, and then
    select **Organizational Unit**.

![](./media/image56.png)

4.  In the **New-Object - Organizational Unit** dialog box,
    type !!**Entra clients**!! and then select **OK**.

![A screenshot of a computer Description automatically
generated](./media/image57.png)

5.  In the navigation pane, select **Seattle Clients**. Right-click on
    **SEA-CL2** and then select **Move**.

![](./media/image58.png)

6.  In the **Move** dialog box, select **Entra clients** and then
    select **OK**.

![A screenshot of a computer Description automatically
generated](./media/image59.png)

7.  Close **Active Directory Users and Computers**.

![A screenshot of a computer Description automatically
generated](./media/image60.png)

**Task 2: Re-configure Entra Connect**

1.  On [SEA-SVR1](https://labclient.labondemand.com/Instructions/e7cc4ae1-e3d9-4c55-accc-696f537e1e17?rc=10),
    double-click Azure AD Connect on the Desktop

![A black rectangle with blue lines Description automatically
generated](./media/image61.png)

2.  In the **Microsoft Azure Active Directory Connect** window
    select **Configure**.

![](./media/image62.png)

3.  On the **Additional tasks** page, select **Customize synchronization
    options** and select **Next**.

![A screenshot of a computer Description automatically
generated](./media/image63.png)

4.  On the **Connect to Entra** page, in
    the **USERNAME** and **PASSWORD** boxes, enter your **Office 365
    Tenant credentials** and then select **Next**.

![A screenshot of a computer Description automatically
generated](./media/image64.png)

5.  On the **Connect your directories** page, click on the Next button.

![A screenshot of a computer Description automatically
generated](./media/image65.png)

6.  On the **Domain and OU filtering** page, ensure that **Sync selected
    domains and Ous** is selected.

7.  Expand **Contoso.com**, select **Entra clients,** and then click
    on **Next**.

![A screenshot of a computer Description automatically
generated](./media/image66.png)

8.  On the **Optional features** page, ensure that **Password hash
    synchronization** is selected, and then select **Next**.

9.  On the **Ready to configure** page, ensure that the **Start the
    synchronization process when configuration completes** is selected,
    and then select **Configure**.

![A screenshot of a computer Description automatically
generated](./media/image67.png)

10. When the configuration is complete, select **Exit**.

![](./media/image68.png)

Note: Wait for approximately 5 minutes for the synchronization to
complete.

**Task 3: Configure Microsoft Entra hybrid Join using Azure AD Connect**

1.  On [SEA-SVR1](https://labclient.labondemand.com/Instructions/e7cc4ae1-e3d9-4c55-accc-696f537e1e17?rc=10)
    VM **Desktop**, double-click on **Azure AD Connect**.

![Text Description automatically generated with medium
confidence](./media/image69.png)

2.  In the **Welcome to Microsoft Entra connect Connect** window,
    select **Configure**.

![](./media/image70.png)

3.  On the **Additional tasks** page, select **Configure device
    options** and select **Next**.

![](./media/image71.png)

4.  On the **Overview** page, select **Next**.

![A screenshot of a computer Description automatically
generated](./media/image72.png)

5.  On the **Connect to Entra** page, enter the Admin Tenant password
    into the **PASSWORD** box, then select **Next**.

![](./media/image73.png)

6.  On the **Device options** page, select **Configure Hybrid Azure AD
    Join**, and then select **Next**.

![A screenshot of a computer Description automatically
generated](./media/image74.png)

7.  On the **Device operating systems** page, select **Windows 10 or
    later domain-joined devices**, and then select **Next**.

![A screenshot of a computer Description automatically
generated](./media/image75.png)

8.  On the **SCP configuration** page, select the check box next
    to **Contoso.com**. Select **Azure Active Directory** from
    the **Authentication Service** dropdown and select **Add**.

![](./media/image76.png)

9.  In the **Enterprise Admin Credentials** window
    enter **Contoso\Administrator** as **Username** and !!**Pa55w.rd**!! as **Password**.
    Select **OK** and select **Next**.

![A screenshot of a computer security Description automatically
generated](./media/image77.png)

![](./media/image78.png)

10. In the **Ready to configure** page, select **Configure** to run the
    configuration.

![A screenshot of a computer Description automatically
generated](./media/image79.png)

11. When the configuration is complete, select **Exit**.

![A screenshot of a computer Description automatically
generated](./media/image80.png)

12. On the taskbar, right-click on **Windows Start button icon** and
    select **Windows Powershell (Admin)**.

![A screenshot of a computer Description automatically
generated](./media/image81.png)

13. In the **Windows PowerShell** window, type the following command,
    and then press **Enter**:

!!**Start-ADSyncSyncCycle -PolicyType Initial**!!

![A screenshot of a computer Description automatically
generated](./media/image82.png)

14. Close the PowerShell window.

Note: Wait for approximately 5 minutes for the synchronization to
complete.

**Task 4: Verify the Entra registration**

1.  Switch
    to [SEA-CL2](https://labclient.labondemand.com/Instructions/e7cc4ae1-e3d9-4c55-accc-696f537e1e17?rc=10).

2.  At the sign-in page, select the **Power** button and then
    select **Restart**.

![Graphical user interface, application Description automatically
generated](./media/image83.png)

***Note**: The reboot will trigger the hybrid Microsoft Entra Join
On [SEA-CL2](https://labclient.labondemand.com/Instructions/e7cc4ae1-e3d9-4c55-accc-696f537e1e17?rc=10).*

3.  After **SEA-CL2** has restarted, sign in
    as **Contoso\Administrator** with the password of !!**Pa55w.rd**!!

![Graphical user interface, application Description automatically
generated](./media/image84.png)

4.  On the taskbar, right-click on **Windows Start icon button** and
    select **Windows Terminal (Admin)**.

![A screenshot of a computer Description automatically
generated](./media/image81.png)

5.  In the **Windows PowerShell** window, type the following command,
    and then press **Enter**:

!!**dsregcmd /status**!!

6.  In the output under **Device State**, verify that. 

- **AzureAdJoined : YES** 

- **DomainJoined : YES** are displayed.

![](./media/image85.png)

***Note: If the device is not yet joined to Entra wait for the Entra
Connect sync to complete and restart SEA-CL2 again. It might take 5-10
minutes for the status to update.***

Additionally you can login to **SEA-SVR1** and in the **Windows
PowerShell** window, type the following command to speed up
synchronization.

!!**Start-ADSyncSyncCycle -PolicyType Initial**!!

7.  Close all windows
    On [SEA-CL2](https://labclient.labondemand.com/Instructions/e7cc4ae1-e3d9-4c55-accc-696f537e1e17?rc=10) and
    sign out.

8.  Switch
    to [SEA-SVR1](https://labclient.labondemand.com/Instructions/e7cc4ae1-e3d9-4c55-accc-696f537e1e17?rc=10) and
    move to **Microsoft Entra admin center** window, navigate and click
    on **Identity**.

![A screenshot of a computer Description automatically
generated](./media/image7.png)

9.  Under the **Identity** section, select **Devices**, then navigate
    and click on **All devices** as shown in the below image.

![A screenshot of a computer Description automatically
generated](./media/image8.png)

10. Verify that **SEA-CL2** has **Microsoft Entra** **hybrid joined** as
    value for the row **Join type**. Click on the **Refresh** button if
    SEA-CL2 is not listed.

![A screenshot of a computer Description automatically
generated](./media/image86.png)

11. Close all windows
    on [SEA-SVR1](https://labclient.labondemand.com/Instructions/e7cc4ae1-e3d9-4c55-accc-696f537e1e17?rc=10).

**Results**: After completing this exercise, you will have successfully
configured and validated Microsoft Entra hybrid join.
