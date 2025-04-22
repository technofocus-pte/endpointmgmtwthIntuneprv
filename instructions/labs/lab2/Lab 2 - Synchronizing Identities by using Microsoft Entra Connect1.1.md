Lab 02 - Synchronizing Identities by using Microsoft Entra Connect

**Summary**

In this lab, you will configure synchronization from Active Directory
Domain Services to Microsoft Entra ID

**Scenario**

Contoso Corporation is currently managing users in both AD DS and
Microsoft Entra ID as separate processes. This is time-consuming and has
led to inconsistent information. You have been tasked with addressing
this issue by connecting the two directories by using the Microsoft
Entra Connect synchronization tool.

**Task 0: Enable TLS 1.2 using PowerShell script**

1.  On **SEA-SVR1**, sign in as **Contoso\Administrator** with the
    password of **Pa55w.rd**

2.  On the start menu
    type PowerShell right click on
    PowerShell and select **run as administrator**.

    ![](./media/image1.png)

3.  Run the following script on the PowerShell.
 
    ```              
        If (-Not (Test-Path 'HKLM:\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319'))
        {
            New-Item 'HKLM:\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319' -Force | Out-Null
        }
        New-ItemProperty -Path 'HKLM:\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319' -Name 'SystemDefaultTlsVersions' -Value '1' -PropertyType 'DWord' -Force | Out-Null
        New-ItemProperty -Path 'HKLM:\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319' -Name 'SchUseStrongCrypto' -Value '1' -PropertyType 'DWord' -Force | Out-Null

        If (-Not (Test-Path 'HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319'))
        {
            New-Item 'HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319' -Force | Out-Null
        }
        New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319' -Name 'SystemDefaultTlsVersions' -Value '1' -PropertyType 'DWord' -Force | Out-Null
        New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319' -Name 'SchUseStrongCrypto' -Value '1' -PropertyType 'DWord' -Force | Out-Null

        If (-Not (Test-Path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server'))
        {
            New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -Force | Out-Null
        }
        New-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -Name 'Enabled' -Value '1' -PropertyType 'DWord' -Force | Out-Null
        New-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -Name 'DisabledByDefault' -Value '0' -PropertyType 'DWord' -Force | Out-Null

        If (-Not (Test-Path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client'))
        {
            New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -Force | Out-Null
        }
        New-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -Name 'Enabled' -Value '1' -PropertyType 'DWord' -Force | Out-Null
        New-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -Name 'DisabledByDefault' -Value '0' -PropertyType 'DWord' -Force | Out-Null
    
        Write-Host 'TLS 1.2 has been enabled. You must rest art the Windows Server for the changes to take affect.' -ForegroundColor Cyan
    ```
    ![](./media/image2.png)

4.  Restart the Windows Server VM.

    ![](./media/image3.png)

**Task 1: Configure directory synchronization with Microsoft Entra Connect**

1.  On ***SEA-SVR1***, if necessary, sign in
    as **Contoso\Administrator** with the
    password of !!Pa55w.rd!!

2.  On the taskbar, select **Microsoft Edge**.

3.  In the address bar,
    enter !!http://www.microsoft.com/en-us/download/details.aspx?id=47594!!

4.  On the Microsoft Entra Connect page, select **Download**.

     Microsoft Entra Connect automatically downloads to
     the **Downloads** folder on **SEA-SVR1**.

     ![A screenshot of a computer Description automatically
     generated](./media/image4.png)

5.  Click on **Open file** for the downloaded
    file **AzureADConnect.msi**.

     ![A screenshot of a phone Description automatically
     generated](./media/image5.png)

6.  In the **Microsoft Azure Active Directory Connect** wizard, on
    the **Welcome to Azure AD Connect** page, select the **I agree to
    the license terms and privacy notice** check box, and then
    select **Continue**.

     ![A screenshot of a computer AI-generated content may be
     incorrect.](./media/image6.png)

7.  On the **Express Settings** page, select **Customize**.

     ![](./media/image7.png)

8.  On the **Install required components** page, select **Install**.

     ![](./media/image8.png)

9.  On the **User sign-in** page, ensure that **Password Hash
    Synchronization** is selected, and then select **Next**.

     ![](./media/image9.png)

10. On the **Connect to Azure AD** page, in
    the **USERNAME** and **PASSWORD** boxes, enter your **Office 365
    Tenant credentials** and then select **Next**.

     ![](./media/image10.png)

11. On the **Connect your directories** page, ensure
    that **Contoso.com** is listed under **FOREST**, and then
    select **Add Directory**.

     ![A screenshot of a computer AI-generated content may be
     incorrect.](./media/image11.png)

12. In the **AD forest account** window, select the **Create New AD
    Account** option, and in the **ENTERPRISE ADMIN USERNAME** field,
    type !!Contoso\Administrator!!, and then
    type !!Pa55w.rd!! in
    the **PASSWORD** field. Select **OK**, and then select **Next**.

     ![A screenshot of a computer screen Description automatically
     generated](./media/image12.png)

     ![A screenshot of a computer AI-generated content may be
     incorrect.](./media/image13.png)

     ![A screenshot of a computer AI-generated content may be
     incorrect.](./media/image14.png)

13. On the **Azure AD sign-in configuration** page, ensure that in
    the **USER PRINCIPAL NAME** drop-down list,
    the **userPrincipalName** value is selected.

     ![](./media/image15.png)

14. Select **Continue without matching all UPN suffixes to verified
    domains** and then select **Next**.

15. On the **Domain and OU filtering** page, select **Sync selected
    domains and OUs**.

16. Expand **Contoso.com**, clear the checkbox next
    to **Contoso.com** and ensure that the only following check boxes
    are selected: **IT**, **Managers**, **Marketing**, **Research**,
    and **Sales**. Select **Next**.

     ![A screenshot of a computer AI-generated content may be
     incorrect.](./media/image16.png)

17. On the **Uniquely identifying your users** page, select **Next**.

18. On the **Filter users and devices** page, select **Next**.

19. On the **Optional features** page, review available options, but do
    not make any changes. Ensure that **Password hash
    synchronization** is selected, and then select **Next**.

     ![](./media/image17.png)

20. On the **Ready to configure** page, ensure that **Start the
    synchronization process when configuration completes** is selected,
    and then select **Install**.

     ![A screenshot of a computer AI-generated content may be
     incorrect.](./media/image18.png)

21. When configuration is complete, select **Exit**.

     ![A screenshot of a computer AI-generated content may be
     incorrect.](./media/image19.png)

     **Note**: At this time, synchronization of objects from your local
     Active Directory Domain Services (AD DS) and Microsoft Entra ID
     begins. You should wait approximately 3-4 minutes for this process to
     complete.

22. Close all open windows.

**Task 2: Verify synchronization in Microsoft Entra ID**

1.  In the **Microsoft Edge** open a new tab and navigate to the
    Microsoft Entra admin Center users page -
    !!https://entra.microsoft.com/#view/Microsoft_AAD_UsersAndTenants/UserManagementMenuBlade/~/AllUsers/menuId/**](https://entra.microsoft.com/#view/Microsoft_AAD_UsersAndTenants/UserManagementMenuBlade/~/AllUsers/menuId/!!
    If prompted to sign in use the Office 365 Tenant credentials from
    the Home tab of the Lab interface.

     ![A screenshot of a computer Description automatically
     generated](./media/image20.png)

2.  Verify that you see users from your local AD DS. Ensure that these
    users have the value **Yes** in the **On-premises sync
    enabled** column.

     ![](./media/image21.png)

3.  In the Navigation pane, select Expand **Groups** and then select
    **All groups**.

     ![A screenshot of a computer Description automatically
     generated](./media/image22.png)

4.  Verify that you see groups from your local AD DS ()

     ![A screenshot of a computer Description automatically
     generated](./media/image23.png)

5.  Select the **Managers** group.

     ![A screenshot of a computer Description automatically
     generated](./media/image24.png)

6.  On the **Managers** group page, select **Members** and then ensure
    that you see users.

     ![A screenshot of a computer Description automatically
     generated](./media/image25.png)

     ![A screenshot of a group of people Description automatically
     generated](./media/image26.png)

     **Note that you cannot add to or remove members from this group, as it
     is sourced from the local AD DS.**

15. Close Microsoft Edge.

**Results**: After completing this exercise, you will have successfully
configured Microsoft Entra Connect to synchronize identity from Active
Directory Domain Services to Microsoft Entra ID
