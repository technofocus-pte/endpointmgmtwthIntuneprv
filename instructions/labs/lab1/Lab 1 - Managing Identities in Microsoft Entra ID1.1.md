Lab01 - Managing Identities in Microsoft Entra ID

**Summary**

In this lab, you will use the Microsoft Entra admin center to create and
modify users, assign administrative roles, create and modify groups, and
manage license assignments in Microsoft Entra ID.

Exercise 1: Creating users in Microsoft Entra ID

**Scenario**

You need to create user accounts in Microsoft Entra ID for some new
employees that will start next week. 

**Note**: For location use either your local region or United States.

You've also been told that several more employees will be hired over the
next couple of months. You've decided that scripting would be a far more
efficient method of adding a large number of new users. You've decided
to create a PowerShell script and test it out when you create Cody
Godinez's account.

**Task 1: Create users by using the Microsoft Entra admin center**

1.  On SEA-SVR1, sign in
    as Contoso\Administrator with the
    password of !!Pa55w.rd!!.
    ![Screenshot](./media/image1.png)

2.  Open the **Microsoft Edge browser** and navigate to             
    !!https://entra.microsoft.com/#view/Microsoft_AAD_UsersAndTenants/UserManagementMenuBlade/~/AllUsers/menuId/**](https://entra.microsoft.com/#view/Microsoft_AAD_UsersAndTenants/UserManagementMenuBlade/~/AllUsers/menuId/!!

3.  At the Sign-in prompt, enter the **Office 365 Tenant credentials**
    from the Home tab of the Lab interface.

    ![A screenshot of a computer Description automatically generated](./media/image2.png)

    **Note** – If promoted for MFA, complete the MFA sign in process.

4.  In the **Microsoft Entra admin center**, expand **Identity** and in
    the navigation pane, select **Users**.

    ![A screenshot of a computer Description automatically generated](./media/image3.png)

     Take note of the users that already exist as members of the Microsoft
     Entra ID domain. Each user is enabled as indicated on the **Account
     enabled** column. The **On-premises synced** **enabled** column
     states **No** for all current users. This indicates that each user was
     created directly in Microsoft Entra ID and not synchronized from an
     on-premises directory service.

     ![A screenshot of a computer Description automatically generated](./media/image4.png)

5.  On the **Users | All users** page, select **New user** then
    select **Create new user**.

     ![](./media/image5.png)

6.  On the **New User** page, ensure that **Create user** is selected,
    enter the following:

    - User principal name: !!ereeve!!

   - Display Name: !!Edmund Reeve!!

   - Uncheck **Auto-generate password.**

   - Password !!P@55w.rd1234!!

    ![A screenshot of a computer Description automatically generated](./media/image6.png)

7.  On the **Properties** tab, provide the below information and then
    click on **Next Assignments.**

    - **Job title**, enter !!HR Rep!!

    - **Department**, enter  !!HR!!

    - **Usage location - United States**

    ![](./media/image7.png)

8.  On the Assignments tab, click on **Review + create** button.

    ![A screenshot of a computer Description automatically generated](./media/image8.png)

9.  Verify the details and then click on the **Create** button.

    ![](./media/image9.png)

    ![A close-up of a computer screen Description automatically generated](./media/image10.png)

10. Similarly create the user account for Miranda Snider with the below
    details.

    - User principal name: !!msnider!!

    - Display Name: !!Miranda Snider!!

    - Uncheck **Auto-generate password.**

    - Password: !!P@55w.rd1234!!

    - Job title - !!Helpdesk Manager!!

    - Department: !!Operations!!
  
    - Usage location: **United States**

11. Select the user account of **Allan Deyoung** and click on **Edit
    properties** and update the Job information with the below details
    and then click on the **Save** button.

    - Job title- !!IT Admin!!
    -  Department - !!IT!!

    ![A screenshot of a computer Description automatically generated](./media/image11.png)

12. Select the user account of **Joni Sherman** and click on **Edit
    properties** and update the Job information with the below details
    and then click on the **Save** button.

    - Job title- !!ParaLegal!!

    -  Department - !!Legal!!

   ![A screenshot of a computer Description automatically
   generated](./media/image12.png)

13. Select the user account of **Alex Wilber** and click on **Edit
    properties** and update the Job information with the below details
    and then click on the **Save** button.

    - Job title - !!Marketing Assistant!!

    -  Department – !!Marketing!!

    ![](./media/image13.png)

**Task 2: Create users by using PowerShell**

1.  On **SEA-SVR1**, on the taskbar,
    right-click **Start**, and then select **Windows PowerShell
    (Admin)**.

    ![](./media/image14.png)

2.  In the **Windows PowerShell** window, type the following command,
    and then press **Enter**. If prompted, enter 
    !\![**Y**](urn:gd:lg:a:send-vm-keys)!!  at the NuGet and repository
    messages:

    !!Install-Module MSOnline!!

    ![](./media/image15.png)

3.  In the **Windows PowerShell** window, type the following command,
    and then press **Enter**:

    !!Connect-MsolService!!
    ![A screenshot of a computer Description automatically generated](./media/image16.png)

4.  In the **Sign in to your account** dialog box, sign in using the
    Office 365 Tenant credentials from the Home tab.
    
    **Note – If you had been prompted to change the Tenant admin credentials password, ensure to provide the updated password.**

5.  In the **Windows PowerShell** window, type the following code to
    create a new user, and then press **Enter**.

     Note – paste the below command in notepad and substitute the Tenant
     details then copy and paste the command in Windows PowerShell, if
     required to ensure the tenant information is correct

    
  ```
  New-MsolUser -UserPrincipalName cgodinez@M365xXXXXXXXX.onmicrosoft.com -DisplayName "Cody Godinez"  FirstName "Cody" -LastName "Godinez" -Password ‘P@55w.rd1234’
  ForceChangePassword $false -UsageLocation "US" -Title "Sales Rep" Department "Sales"
 ```
 

   ![A screenshot of a computer screen Description automatically generated](./media/image17.png)

6.  In the **Windows PowerShell** window, type the following command to
    reset the passwords of the Alew Wilber, Allan Deyoung and Joni
    Sherman

>   #  
        Get-MsolUser | Where-Object DisplayName -EQ "Alex Wilber" |
        Set-MsolUserPassword -NewPassword P@55w.rd1234 -ForceChangePassword
        $false
>   #
    
        Get-MsolUser | Where-Object DisplayName -EQ “Allan Deyoung” |
        Set-MsolUserPassword -NewPassword P@55w.rd1234 -ForceChangePassword
        $false
>   #
    
        Get-MsolUser | Where-Object DisplayName -EQ "Joni Sherman" |
        Set-MsolUserPassword -NewPassword P@55w.rd1234 -ForceChangePassword
        $false
>
> ![A computer screen shot of a program Description automatically
> generated](./media/image18.png)

7.  In the **Windows PowerShell** window, type the following command,
    and then press **Enter**:

>   #
        Get-MsolUser

8.  Verify that the list of users from your tenant is displayed. Also
    take note of which users have a license assigned. Any user with
    the **isLicensed** value of **False** has not been assigned a
    license.

> ![A screenshot of a computer Description automatically
> generated](./media/image19.png)

**Results**: After completing this exercise, you will have successfully
created new user accounts in Microsoft Entra ID.

Exercise 2: Assigning Administrative Roles in Microsoft Entra ID

**Scenario**

You need to review and modify the current administrative roles for your
tenant.

You have been provided a list of users should have administrative roles
assigned as indicated in the following table.

[TABLE]

Task 1: Review and Assign Administrative Roles

1.  On [***SEA-SVR1***](urn:gd:lg:a:select-vm), switch to **Microsoft
    Edge**.

2.  In the **Microsoft Entra admin center**, in the Navigation pane,
    expand **Roles & admins.**

3.  Select **Roles & admin** and search for !!**Global administrator**!!
    and click on the Role **Global Administrator**.

> ![A screenshot of a computer Description automatically
> generated](./media/image20.png)

4.  Click on **Add assignments**.

> ![A screenshot of a computer Description automatically
> generated](./media/image21.png)

5.  On the Add assignments page, select **Allan Deyoung** and then
    select **Add**.

> ![A screenshot of a computer Description automatically
> generated](./media/image22.png)

6.  At the top of the page, in the navigation link, select **Roles and
    administrators**.

> ![A screenshot of a computer Description automatically
> generated](./media/image23.png)

7.  On the **Roles and administrators** page, search and select !!**User
    administrator**!!. Ensure that **Assignments** is selected.

> ![A screenshot of a chat Description automatically
> generated](./media/image24.png)
>
> Notice that there are no users currently assigned to the User
> administrator role.

8.  Click on + **Add assignments**.

> ![A screenshot of a computer Description automatically
> generated](./media/image25.png)

9.  On the Add assignments page, select **Edmund Reeve** and then
    select **Add**.

> ![A screenshot of a computer Description automatically
> generated](./media/image26.png)

10. Click on **Roles and administrators** link, then search and
    select !!**Helpdesk administrator**!!.

> ![A screenshot of a computer Description automatically
> generated](./media/image27.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image28.png)
>
> Notice that there are no users currently assigned to the Helpdesk
> administrator role.

11. On the **Helpdesk administrator | Assignments** page, select **Add
    assignments**.

> ![A screenshot of a computer Description automatically
> generated](./media/image29.png)

12. On the Add assignments page, select **Miranda Snider** and then
    select **Add**.

> ![A screenshot of a computer Description automatically
> generated](./media/image30.png)

13. At the top of the page, in the navigation link, select **Roles and
    administrators**.

> ![A screenshot of a computer Description automatically
> generated](./media/image31.png)

**Results**: After completing this exercise, you should have
successfully assigned administrative roles to users.

Exercise 3: Creating and managing groups and validating license
assignment.

**Scenario**

You need to add the three new users to a Security group and assign
licenses as indicated in the following table.

[TABLE]

You have also been asked to modify the Company branding for the sign-in
page.

Task 1: Create groups by using the Microsoft Entra admin center

1.  On [***SEA-SVR1***](urn:gd:lg:a:select-vm), in the **Microsoft Entra
    admin center**, in the navigation pane, expand **Identity** and
    select **Groups** and then click on **New group.**

> ![A screenshot of a computer Description automatically
> generated](./media/image32.png)

2.  On the **New Group** page, enter the following:

    - Group type: **Security**

    - Group name: !\![**Contoso_Managers**](urn:gd:lg:a:send-vm-keys)!!

    - Membership type: **Assigned**

3.  Under Members, click on **No members selected**.

4.  In the Add members page add **Edmund Reeve**, **Miranda Snider**,
    and then click **Select**.

> ![A screenshot of a computer Description automatically
> generated](./media/image33.png)

5.  Select **Create**.

Task 2: Create groups by using PowerShell

1.  On [***SEA-SVR1***](urn:gd:lg:a:select-vm), switch to Windows
    PowerShell.

2.  In the **Windows PowerShell** window, type the following code to
    create a new group, and then press **Enter**:

>   #
        New-MsolGroup -DisplayName "Contoso_Sales" -Description "Contoso
        Sales team users"
>
> ![A screenshot of a computer Description automatically
> generated](./media/image34.png)

3.  In the **Windows PowerShell** window, type the following command,
    and then press **Enter**:

>   #
        Get-MsolGroup
>
> ![A screenshot of a computer screen Description automatically
> generated](./media/image35.png)

4.  Verify that you get the list of groups in your tenant, including the
    **Contoso_Sales** group you just created.

> ![](./media/image36.png)

5.  In the **Windows PowerShell** window, type the following code to
    define a variable as the Contoso_Sales group, and then
    press **Enter**:

>   #
        $group = Get-MsolGroup | Where-Object {$\_.DisplayName -eq
        "Contoso_Sales"}

6.  In the **Windows PowerShell** window, type the following code to
    define another variable as the user, and then press **Enter**:

>   #
        $user = Get-MsolUser | Where-Object {$\_.DisplayName -eq "Cody
        Godinez"}

7.  In the **Windows PowerShell** window, type the following code to add
    Cody to Contoso_Sales using set variables, and then press **Enter**:

>   #
        Add-MsolGroupMember -GroupObjectId $group.ObjectId
        -GroupMemberType "User" -GroupMemberObjectId $user.ObjectId

8.  In the **Windows PowerShell** window, type the following code, and
    then press **Enter**:

>   #
            Get-MsolGroupMember -GroupObjectId $group.ObjectId

9.  Verify that you see **Cody Godinez** in the command output result.

> ![A screenshot of a computer program Description automatically
> generated](./media/image37.png)

10. Close Windows PowerShell.

Task 3: Review licenses and modify company branding

1.  In the Microsoft admin center, in the Navigation pane, expand **Billing** and select **Licenses** or navigate to the following url.

>   #
        https://admin.microsoft.com/Adminportal/Home?referrer=entra#/licenses
>
> ![](./media/image38.png)

2.  On the **Licenses** page, under Subscriptions, check for all the
    available licenses.

> ![](./media/image39.png)
>
> Note - Take note of the current licenses available and assigned
> for **Enterprise Mobility + Security E5** and **Office 365 E5 (no
> Teams)**
>
> ![](./media/image40.png)

3.  In the Microsoft 365 admin center, On the left navigation pane
    select **Users** and then **Active users**.

> ![](./media/image41.png)

4.  In the user list, select **Cody Godinez**.

> ![A screenshot of a computer Description automatically
> generated](./media/image42.png)

5.  On the Cody Godinez page, select **Licenses and apps**

> ![A screenshot of a computer Description automatically
> generated](./media/image43.png)
>
> Notice that Cody does not have any current license assignments.

6.  On the **Licenses and apps** page, select the check box next
    to **Enterprise Mobility + Security E5** and **Office 365 E5 (no
    Teams)** and click on **Save changes**.

> ![A screenshot of a login page Description automatically
> generated](./media/image44.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image45.png)

**Note**: Repeat steps 4 to 8 for assigning licenses Enterprise
Mobility + Security E5 and Office 365 E5 (no Teams) to Joni Sherman,
Alex Wilber and Allan Deyoung in case they aren’t assigned the licenses.

7.  In the Microsoft Entra admin center, in the Navigation pane,
    expand **Identity** and select **Groups**.

> ![](./media/image46.png)

8.  On the **Groups | All groups** page, select **Contoso_Managers**.

> ![A screenshot of a computer Description automatically
> generated](./media/image47.png)

9.  On the **Contoso_Managers** page, select **Licenses**.

> ![](./media/image48.png)
>
> **Notice that the Contoso_Managers group does not have any current
> license assignments.**

10. . Navigate to Microsoft 365 admin center and scroll down to licenses
    select **Enterprise Mobility + Security E5.**

> ![A screenshot of a computer Description automatically
> generated](./media/image49.png)

11. Click on **Groups** tab and click on **Assign licenses.**

> ![](./media/image50.png)

12. Select Contoso_Mangers from the list and click on **Assign.**

13. In the Microsoft admin center, in the Navigation pane, expand **Billing** and select **Licenses**.

> ![A screenshot of a computer Description automatically
> generated](./media/image51.png)![A screenshot of a computer
> Description automatically generated](./media/image52.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image53.png)

14. On the **Licenses|Overview** page, under **Manage**, select **All
    products**.

> ![A screenshot of a computer Description automatically
> generated](./media/image54.png)
>
> ![](./media/image53.png)

15. Repeat the same process and assign Office 365 E5 (no Teams) license
    to Contoso_Managers team.

> Take note of the users that are assigned the Office 365 E5 (no Teams)
> license. Notice the Assignment Paths column which indicates how
> license assignment is configured for each user. Edmund and Miranda
> both receive their license assignment from their membership in the
> Contoso_Managers group. You may need to select **Refresh** a couple of
> times to update the Assignment path column.
>
> ![](./media/image55.png)

16. Close Microsoft Edge.

**Results**: After completing this exercise, you should have
successfully created and managed groups, and assigned licenses.
