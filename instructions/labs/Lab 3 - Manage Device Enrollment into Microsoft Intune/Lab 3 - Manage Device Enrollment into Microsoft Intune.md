**Lab 3 - Manage Device Enrollment into Microsoft Intune**

**Summary**

In this lab, you prepare for device management using Microsoft Intune by
reviewing and assigning licenses, configuring Windows automatic
enrollment, and configuring enrollment restrictions.

**Prerequisites**

To following lab(s) must be completed before this lab:

- Lab \#1-Managing Identities in Microsoft Entra ID

**Scenario**

You need to prepare for device management using Microsoft Intune. First
of all, you need to ensure that users are assigned appropriate licenses
for device management. As a verification test, you will assign Aaron
Nicholls the required licenses. You also need to ensure that any Windows
device that is joined or registered to Microsoft Entra ID will
automatically be enrolled into Intune. You have also been asked to
ensure that members of the Sales group are restricted from enrolling
personal Android and iOS devices into Intune and that the Enrollment
Device Limit is increased to 10 devices. Finally, you need to configure
Allan Deyoung as a Device enrollment manager to allow him to enroll 1000
devices.

### Task 1: Enable TLS 1.2 using PowerShell script

1.  On **SEA-SVR1**, sign in as **Contoso\Administrator** with the
    password of **Pa55w.rd**

2.  On the start menu
    type [**PowerShell**](urn:gd:lg:a:send-vm-keys) right click on
    PowerShell and select **run as administrator**.

![](media/media/image1.png)

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

![](media/media/image2.png)

4.  Restart the Windows Server VM.

![](media/media/image3.png)

### Task 2: Configure directory synchronization with Microsoft Entra Connect

1.  On [***SEA-SVR1***](urn:gd:lg:a:select-vm), if necessary, sign in
    as [**Contoso\Administrator**](urn:gd:lg:a:send-vm-keys) with the
    password of !\![**Pa55w.rd**](urn:gd:lg:a:send-vm-keys)!!

2.  On the taskbar, select **Microsoft Edge**.

3.  In the address bar, enter !!https://entra.microsoft.com!!, expand
    Entra ID, then select Entra Connect

> ![](media/media/image4.png)
>
> ![](media/media/image5.png)

4.  On the Microsoft Entra Connect page, go to manage tab
    select **Download Connect Sync Agent**.

> ![](media/media/image6.png)
>
> ![](media/media/image7.png)
>
> Click on **Accept terms & download.** Microsoft Entra Connect
> automatically downloads to the **Downloads** folder on **SEA-SVR1**.
>
> ![](media/media/image8.png)

5.  Click on **Open file** for the downloaded
    file **AzureADConnect.msi**.

> ![A screenshot of a phone Description automatically
> generated](media/media/image9.png)

6.  In the **Microsoft Entra Connect Sync** wizard, on the **Welcome to
    Microsoft Entra Connect Sync** page, select the **I agree to the
    license terms and privacy notice** check box, and then
    select **Continue**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](media/media/image10.png)

7.  On the **Express Settings** page, select **Customize**.

> ![](media/media/image11.png)

8.  On the **Install required components** page, select **Install**.

> ![](media/media/image12.png)

9.  On the **User sign-in** page, ensure that **Password Hash
    Synchronization** is selected, and then select **Next**.

> ![](media/media/image13.png)

10. On the **Connect to Azure AD** page, in
    the **USERNAME** and **PASSWORD** boxes, enter your **Office 365
    Tenant credentials** and then select **Next**.

> ![](media/media/image14.png)

11. On the **Connect your directories** page, ensure
    that **Contoso.com** is listed under **FOREST**, and then
    select **Add Directory**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](media/media/image15.png)

12. In the **AD forest account** window, select the **Create New AD
    Account** option, and in the **ENTERPRISE ADMIN USERNAME** field,
    type [**Contoso\Administrator**](urn:gd:lg:a:send-vm-keys), and then
    type !\![**Pa55w.rd**](urn:gd:lg:a:send-vm-keys)!! in
    the **PASSWORD** field. Select **OK**, and then select **Next**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](media/media/image16.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](media/media/image17.png)

13. On the **Microsoft Entra sign-in configuration** page, ensure that
    in the **USER PRINCIPAL NAME** drop-down list,
    the **userPrincipalName** value is selected.

> ![](media/media/image18.png)

14. Select **Continue without matching all UPN suffixes to verified
    domains** and then select **Next**.

15. On the **Domain and OU filtering** page, select **Sync selected
    domains and OUs**.

16. Expand **Contoso.com**, clear the checkbox next
    to **Contoso.com** and ensure that the only following check boxes
    are selected: **IT**, **Managers**, **Marketing**, **Research**,
    and **Sales**. Select **Next**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](media/media/image19.png)

17. On the **Uniquely identifying your users** page, select **Next**.

18. On the **Filter users and devices** page, select **Next**.

19. On the **Optional features** page, review available options, but do
    not make any changes. Ensure that **Password hash
    synchronization** is selected, and then select **Next**.

> ![](media/media/image20.png)

20. On the **Ready to configure** page, ensure that **Start the
    synchronization process when configuration completes** is selected,
    and then select **Install**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](media/media/image21.png)

21. When configuration is complete, select **Exit**.

> ![](media/media/image22.png)
>
> **Note**: At this time, synchronization of objects from your local
> Active Directory Domain Services (AD DS) and Microsoft Entra ID
> begins. You should wait approximately 3-4 minutes for this process to
> complete.

22. Close all open windows.

**Task 3: Review and assign licenses for device management**

1.  On [*SEA-SVR1*](https://labclient.labondemand.com/Instructions/e7cc4ae1-e3d9-4c55-accc-696f537e1e17?rc=10),
    navigate to **Microsoft 365 admin center** window.

![](media/media/image23.png)

2.  Navigate and select **Billing**, then click on **Licenses**.

![A screenshot of a computer AI-generated content may be
incorrect.](media/media/image24.png)

3.  In the **Licenses** page, take note of the licenses that are
    available in the tenant.

![A screenshot of a computer AI-generated content may be
incorrect.](media/media/image25.png)

4.  Select and click on **Enterprise Mobility + Security E5**. Notice
    all the users that have been assigned this license. You can assign
    and remove licenses from this location.

![A screenshot of a computer AI-generated content may be
incorrect.](media/media/image26.png)

![](media/media/image27.png)

5.  Select a user to see the licenses assigned to the user. Take note of
    the services included in the Enterprise Mobility + Security E5
    license. **Microsoft Intune** is one of the supported services for
    this license.

![](media/media/image28.png)

6.  In the **Microsoft 365 admin center** navigation pane,
    select **Users,** then select **Active users**.

![](media/media/image29.png)

7.  Search and select !!**Cindy White**!!

![](media/media/image30.png)

8.  On **Cindy White user** page, click on **Licenses and apps**. Ensure
    that the **Usage location** field, is set to **United
    States** and the following licenses **Enterprise Mobility + Security
    E5 and Office 365 E5 (no teams)** are assigned.

![](media/media/image31.png)

**Task 4: Setting Password of the user utilizing PowerShell**

1.  In [***SEA-SVR1***](urn:gd:lg:a:select-vm), right-click on **Start
    button**, and then select **Windows PowerShell (Admin)**.

![](media/media/image32.png)

2.  On **User Account Control** dialog box, select **Yes**.

![](media/media/image33.png)

3.  In the **Windows PowerShell** window, type the following command,
    and then press **Enter**:

!!**Connect-MgGraph -Scopes “User.Read.All”**!!

![](media/media/image34.png)

4.  In the **Sign in to your account** dialog box, sign in using the
    Office 365 Tenant credentials from the Home tab.

**Note – If you had been prompted to change the Tenant admin credentials
password, ensure to provide consent.**

5.  In the **Windows PowerShell** window, type the following command to
    reset the passwords of the **Cindy White**

!!**Get-MgUser -Filter "displayName eq 'Cindy White'" |**

> **ForEach-Object {**
>
> **Update-MgUser -UserId $\_.Id -PasswordProfile @{**
>
> **Password = "P@55w.rd1234"**
>
> **ForceChangePasswordNextSignIn = $false**
>
> **}**
>
> **}**!!

![](media/media/image35.png)

**Task 5: Enable Windows Automatic Enrollment into Microsoft Intune**

1.  In **SEA-SVR1**, open a new tab in **Microsoft Edge**, and then in
    the address bar type !!**https://Endpoint.microsoft.com**!! and then
    press **Enter**.

![](media/media/image36.png)

2.  In the Microsoft Intune admin center, select **Devices**.

![](media/media/image37.png)

3.  Navigate and click on **Enrollment**. Ensure that **Windows** tab is
    select, then navigate to **Enrollment options** section and click on
    **Automatic Enrollment**.

![](media/media/image38.png)

4.  On the **MDM user scope** row, select **All** radio button and then
    select **Save**.

![](media/media/image39.png)

5.  Click on **Devices | Enrollment** link as shown in the below image.

![](media/media/image40.png)

**Note**: By performing this step, you enabled automatic enrollment into
Intune for any User that performs an Azure AD join with a Windows
device.

**Task 6: Configure Enrollment Restrictions**

1.  Navigate to **Devices onboarding** section and click on
    **Enrollment**. Then, click on **Android** tab as shown in the below
    image.

![](media/media/image41.png)

2.  Scroll down to **Enrollment options** section and click on **Device
    platform restriction**.

![](media/media/image42.png)

3.  Select **Android restrictions** tab, then select +**Create
    restriction**.

![](media/media/image43.png)

![](media/media/image44.png)

4.  On the **Create restriction** page, in the **Name** box,
    enter !!**Android Personal Device Restriction**!! Select **Next**.

![](media/media/image45.png)

5.  On the Platform settings page, under **Personally owned devices**,
    select **Block**  and click on the **Next** button:

![](media/media/image46.png)

6.  On the **Scope tags** page, select **Next**.

![](media/media/image47.png)

7.  On the **Assignments** page, under **Included groups**, select **Add
    groups**.

![](media/media/image48.png)

8.  In **Select groups to include** pane **Search bar**, type and select
    **Sales**, then click on the **Select** button.

![](media/media/image49.png)

9.  In the **Assignments** tab, click on the **Next** button.

![A screenshot of a computer Description automatically
generated](media/media/image50.png)

10. On the **Review + create** page, select **Create**.

![A screenshot of a computer Description automatically
generated](media/media/image51.png)

Notice the Android Personal Device Restriction assigned with a priority
of 1.

![A screenshot of a computer Description automatically
generated](media/media/image52.png)

11. In the **Devices | Enrollment** page, in the **Windows** tab,
    navigate to **Enrollment options** section and click on the **Device
    limit restriction**.

![A screenshot of a computer Description automatically
generated](media/media/image53.png)

Notice that there is a Default device limit restriction that is assigned
to All Users. This default restriction sets a device enrollment limit to
5 devices per user.

12. In the **Enrollment device limit restrictions**, select + **Create
    restriction**.

![A screenshot of a computer Description automatically
generated](media/media/image54.png)

13. On the Create restriction page, in the **Name** box, enter !!**Sales
    Device Enrollment Limit**!! Select **Next**.

![A screenshot of a computer Description automatically
generated](media/media/image55.png)

14. On the **Device limit** page, select **10**, and then
    select **Next**.

![A screenshot of a computer Description automatically
generated](media/media/image56.png)

15. On the **Scope tags** page, select **Next**.

![A screenshot of a computer Description automatically
generated](media/media/image57.png)

16. On the **Assignments** page, under **Included groups**, select **Add
    groups**.

![A screenshot of a computer Description automatically
generated](media/media/image58.png)

17. In the **Select groups to include** page search box type and select
    **Sales** and then click on **Select** button.

![](media/media/image59.png)

18. Click on the **Next** button.

![A screenshot of a computer Description automatically
generated](media/media/image60.png)

19. On the **Review + create** page, select **Create**.

![A screenshot of a computer Description automatically
generated](media/media/image61.png)

20. Reload the page. Notice the Sales Device Enrollment Limit,
    configured with a Device limit of 10.

![](media/media/image62.png)

### Task 7: Configure a Device enrollment manager

1.  In the **Microsoft Intune admin center**, select **Devices**.

![](media/media/image63.png)

2.  Navigate to **Device onboarding** section and click on
    **Enrollment**, then click on **Device enrolment managers** tab.

![](media/media/image64.png)

3.  On the **Enroll devices** pane, select **Device enrollment
    managers**.

Notice that, by default, there are no Device enrollment managers
configured.

4.  On the **Enroll devices|Device enrollment managers** page,
    select **Add**.

![A screenshot of a computer Description automatically
generated](media/media/image65.png)

5.  In the **Add user** page, under User name, enter the email address
    of Allan [DeYoung
     !!**AllanD@M365xXXXXXXX.onmicrosoft.com**](mailto:DeYoung !!AllanD@M365xXXXXXXX.onmicrosoft.com)!!
     (substitute **XXXXXX** with your tenant name) and then
    select **Add**.

![A screenshot of a computer Description automatically
generated](media/media/image66.png)

**Allan is now allowed to enroll up to 1000 devices.**

6.  In the Microsoft Intune admin center, in the navigation pane,
    select **Home**.

![A screenshot of a computer Description automatically
generated](media/media/image67.png)

7.  Close Microsoft Edge.

**Results**: After completing this exercise, you will have successfully
reviewed and assigned licenses, configured Windows automatic enrollment,
enabled and assigned enrollment restrictions, and configured a Device
enrollment manager.
