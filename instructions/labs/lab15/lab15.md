Lab 15 - Configuring Multi-factor Authentication

**Summary**

In this lab, you will configure per-user multi-factor authentication
(MFA) and apply MFA using a conditional access policy.

Exercise 1: Configure per-user multi-factor authentication.

**Scenario**

To provide additional security for user sign on events, you need to
configure and test multi-factor authentication (MFA). You decide to
first test out per-user MFA. Alex Wilber has agreed to validate the
settings for you.

Task 1: Validate sign-in before enabling MFA

1.  Switch and sign in
    to [**SEA-WS3**](urn:gd:lg:a:select-vm) as !\![**Admin**](urn:gd:lg:a:send-vm-keys)!!
    with the password !\![**Pa55w.rd**](urn:gd:lg:a:send-vm-keys)!!

2.  On the taskbar, select **Microsoft Edge**. In the address bar,
    enter !\![**outlook.office.com**](urn:gd:lg:a:send-vm-keys)!!  and
    press Enter.

3.  At the **Sign in** page,
    enter !!**AlexW@M365xXXXXXXX.onmicrosoft.com**!!  and then
    select **Next**.

4.  On the **Enter password** page, enter !!**P@55w.rd1234**!! and
    select **Sign in**. At the Edge Save password prompt,
    select **Save**.

> Outlook on the Web opens. Take note that only the password was
> required to sign in to Outlook on the Web.

5.  At the top-right corner, select the **Account manager for Alex
    Wilber** and then select **Sign out**.

> ![](./media/image1.png)

6.  Close Microsoft Edge.

Task 2: Enable MFA for a user

1.  Switch to [**SEA-SVR1**](urn:gd:lg:a:select-vm).
    On [**SEA-SVR1**](urn:gd:lg:a:select-vm), if necessary, sign in
    as [**Contoso\Administrator**](urn:gd:lg:a:send-vm-keys) with the
    password of !! [**Pa55w.rd**](urn:gd:lg:a:send-vm-keys)!!  and
    close **Server Manager**.

2.  On the taskbar select **Microsoft Edge**, navigate to **Microsoft
    Entra admin center** !!**https://Entra.Microsoft.com**!!

3.  Sign in with **Office 365 Tenant admin** credentials.

> ![A screenshot of a computer Description automatically
> generated](./media/image2.png)
>
> The **Microsoft Entra admin center** opens.

4.  In the **Microsoft Entra admin center**, in the navigation pane,
    expand **Identity**, then select **Users**.

5.  Select **All users** and then at the top of the results pane
    select **Per-user MFA**. You may need to select the ellipse first to
    view the **Per-user MFA** option.

> ![A screenshot of a computer Description automatically
> generated](./media/image3.png)

6.  On the multi-factor authentication page, select **service
    settings**.

> ![A screenshot of a computer Description automatically
> generated](./media/image4.png)

7.  Scroll down to the **verification options** section.

> Take note of the various methods that can be configured for user
> verification.

8.  In the **remember multi-factor authentication on trusted
    device** section, select the check box next to **Allow users to
    remember multi-factor authentication on devices they trust**.

9.  Next to **Number of days users can trust devices for**,
    enter **30** and then select **save**. Select **close** when
    prompted.

> ![](./media/image5.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image6.png)

10. At the top of the page, under **multi-factor authentication**,
    select **users**.

> ![A screenshot of a computer Description automatically
> generated](./media/image7.png)

11. In the user list, select the check box next to **Alex Wilber**.

12. In the Alex Wilber page, select **Enable**.

> ![A screenshot of a computer Description automatically
> generated](./media/image8.png)

13. On the **About enabling multi-factor auth** message, select **enable
    multi-factor auth**.

> ![A screenshot of a computer Description automatically
> generated](./media/image9.png)

14. On the **Updates successful** message, select **close**. Take note
    that the **Multi-Factor Auth Status** for Alex Wilber is
    now **Enabled**.

> ![A screenshot of a computer Description automatically
> generated](./media/image10.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image11.png)

15. Close Microsoft Edge.

Task 3: Register and Validate MFA

1.  Switch to [**SEA-WS3**](urn:gd:lg:a:select-vm). On the taskbar,
    select **Microsoft Edge**.

2.  In the address bar,
    enter !\![**outlook.office.com**](urn:gd:lg:a:send-vm-keys)!!  and
    press Enter.

3.  On the **Pick an account** page,
    select !\![**AlexW@M365xXXXXXXX.onmicrosoft.com**](mailto:AlexW@M365xXXXXXXX.onmicrosoft.com)!!

> ![A screenshot of a computer Description automatically
> generated](./media/image12.png)

4.  On the **Enter password** page, enter !!**P@55w.rd1234**!! and
    select **Sign in**.

5.  At the **More information required** page, select **Next**. The Keep
    you account secure page opens.

> ![A screenshot of a computer Description automatically
> generated](./media/image13.png)
>
> Typically, you will want to use the Microsoft Authenticator app to
> manage multi-factor authentication. However for this lab scenario, you
> will use text messages.

6.  On the **Keep your account secure** page, select **I want to set up
    a different method**.

> ![A screenshot of a computer Description automatically
> generated](./media/image14.png)

7.  In the **Choose a different method** dialog box, select **Phone**,
    and then select **Confirm**.

> ![A screenshot of a computer Description automatically
> generated](./media/image15.png)

8.  On the **Phone** page, enter your mobile phone number which you can
    receive text messages, and then select **Next**.

> ![A screenshot of a computer screen Description automatically
> generated](./media/image16.png)

9.  After you receive the verification code as a text message, enter the
    code where indicated on the **Phone** page and then select **Next**.

> ![](./media/image17.png)

10. At the SMS verified message, select **Next** and then
    select **Done**.

> ![A screenshot of a computer screen Description automatically
> generated](./media/image18.png)
>
> ![](./media/image19.png)

11. At the Stay signed in message, select **No**.

> ![A screenshot of a computer error Description automatically
> generated](./media/image20.png)
>
> Outlook on the Web opens to Alex Wilber's inbox.

12. At the top-right corner, select the **Account manager for Alex
    Wilber** and then select **Sign out**.

> ![](./media/image21.png)
>
> **Note**: Users only have to register the first time they use MFA.
> Subsequent sign-ins only require providing the validation code which
> it texted to the phone number that you entered during registration.

13. In the address bar,
    enter !\![**outlook.office.com**](urn:gd:lg:a:send-vm-keys)!!  and
    press Enter.

14. On the **Pick an account** page,
    select !!**AlexW@M365xXXXXXXXX.onmicrosoft.com**!!

15. On the **Enter password** page, enter !!**P@55w.rd1234**!! and
    select **Sign in**.

> ![A screenshot of a computer error Description automatically
> generated](./media/image22.png)
>
> The **Verify your identity** prompt opens. Notice that it contains the
> last two digits of your phone number.

16. At the **Verify your identity** prompt, select your Text phone
    number.

17. At the **Enter code** page, enter the code sent to your mobile
    phone, and then select **Verify**.

> ![A screenshot of a computer error message Description automatically
> generated](./media/image23.png)
>
> Notice that you can select a check box to not ask for verification
> again for 30 days.

18. As **Microsoft Authenticator App** ensure more security and smooth
    experience, you will be prompted to configure the same, for now
    click on **Skip for now**

> ![A screenshot of a computer error Description automatically
> generated](./media/image24.png)

19. At the Stay signed in message, select **No**. Outlook on the Web
    opens to Alex Wilber's inbox.

> ![A screenshot of a computer error Description automatically
> generated](./media/image25.png)

20. At the top-right corner, select the **Account manager for Alex
    Wilber** and then select **Sign out**.

> ![A computer screen shot of a computer screen Description
> automatically generated](./media/image26.png)

21. Close Microsoft Edge.

Task 3: Remove per-user MFA

1.  Switch to [**SEA-SVR1**](urn:gd:lg:a:select-vm).
    On [**SEA-SVR1**](urn:gd:lg:a:select-vm), if necessary, sign in
    as [**Contoso\Administrator**](urn:gd:lg:a:send-vm-keys) with the
    password of  !\![**Pa55w.rd**](urn:gd:lg:a:send-vm-keys)!! and
    close **Server Manager**.

2.  On the taskbar select **Microsoft Edge**, navigate to **Microsoft
    Entra admin center** !!**https://Entra.Microsoft.com**!!

3.  Sign in with **Office 365 Tenant admin** credentials.

> ![A screenshot of a computer Description automatically
> generated](./media/image2.png)
>
> The **Microsoft Entra admin center** opens.

4.  In the **Microsoft Entra admin center**, in the navigation pane,
    expand **Identity**, then select **Users**.

5.  Select **All users** and then at the top of the results pane
    select **Per-user MFA**. You may need to select the ellipse first to
    view the **Per-user MFA** option.

> ![A screenshot of a computer Description automatically
> generated](./media/image3.png)

6.  At the top of the page, under **multi-factor authentication**,
    select **users**.

7.  In the user list, select the check box next to **Alex Wilber**.

> Take note that the **Multi-Factor Auth Status** for Alex Wilber is now
> set to **Enforced** (was previously set to Enabled). This is because
> Alex has registered and is using MFA.
>
> ![A screenshot of a computer Description automatically
> generated](./media/image27.png)

8.  In the Alex Wilber page, select **Manage user settings.**

> ![A screenshot of a computer Description automatically
> generated](./media/image28.png)

9.  On the Manage user settings box, select the check box next to all
    three options, select **save** and then select **close**.

> ![A screenshot of a computer Description automatically
> generated](./media/image29.png)
>
> These options will remove all saved MFA settings for Alex.
>
> ![A white rectangular frame with black border Description
> automatically generated](./media/image30.png)

10. In the user list, select the check box next to **Alex Wilber**.

11. In the Alex Wilber page, select **Disable**.

> ![A screenshot of a computer Description automatically
> generated](./media/image31.png)

12. On the **Disable multi-factor authentication** message,
    select **yes**.

> ![](./media/image32.png)

13. On the **Updates successful** message, select **close**.

> ![A white screen with black text Description automatically
> generated](./media/image33.png)
>
> Take note that the **Multi-Factor Auth Status** for Alex Wilber is
> now **Disabled**.
>
> ![A screenshot of a computer Description automatically
> generated](./media/image34.png)

14. Close Microsoft Edge.

**Results**: After completing this exercise, you will have successfully
configured per-user multi-factor authentication.

Exercise 2: Configure multi-factor authentication using conditional
access

**Scenario**

To provide additional security for user sign on events, you need to
configure and test multi-factor authentication (MFA). You decide that
using a conditional access policy provides greater flexibility for your
MFA requirements. Alex Wilber has agreed to validate the settings for
you.

Task 1: Validate sign-in before enabling conditional access with MFA

1.  Switch and sign in
    to [**SEA-WS3**](urn:gd:lg:a:select-vm) as !\![**Admin**](urn:gd:lg:a:send-vm-keys)!!
     with the password !\![**Pa55w.rd**](urn:gd:lg:a:send-vm-keys)!!

2.  On the taskbar, select **Microsoft Edge**. In the address bar,
    enter !\![**outlook.office.com**](urn:gd:lg:a:send-vm-keys)!! and
    press Enter.

3.  At the **Sign in** page,
    enter !!**AlexW@M365xXXXXXXX.onmicrosoft.com**!!  and then
    select **Next**.

4.  On the **Enter password** page, enter !!**P@55w.rd1234**!!  and
    select **Sign in**. At the Edge Save password prompt,
    select **Save**.

> Outlook on the Web opens. Take note that only the password was
> required to sign in to Outlook on the Web.

5.  At the top-right corner, select the **Account manager for Alex
    Wilber** and then select **Sign out**.

> ![A screenshot of a computer Description automatically
> generated](./media/image1.png)

6.  Close Microsoft Edge.

Task 2: Configure conditional access with MFA

1.  Switch to [**SEA-SVR1**](urn:gd:lg:a:select-vm).
    On [**SEA-SVR1**](urn:gd:lg:a:select-vm), if necessary, sign in
    as [**Contoso\Administrator**](urn:gd:lg:a:send-vm-keys) with the
    password of  !\![**Pa55w.rd**](urn:gd:lg:a:send-vm-keys)!!  and
    close **Server Manager**.

2.  On the taskbar select **Microsoft Edge**, navigate to **Microsoft
    Entra admin center** !!**https://Entra.Microsoft.com**!!

3.  Sign in with **Office 365 Tenant admin** credentials.

> ![A screenshot of a computer Description automatically
> generated](./media/image2.png)
>
> The **Microsoft Entra admin center** opens.

4.  In the **Microsoft Entra admin center**, in the navigation pane,
    expand **Identity**, then expand **Protection**, then **Conditional
    Access.**

> ![A screenshot of a computer Description automatically
> generated](./media/image35.png)

5.  On the **Conditional Access** page, select **Policies**, then select
    **+ New policy**.

> ![A screenshot of a computer Description automatically
> generated](./media/image36.png)

6.  On the **New Conditional access policy** page, in the **Name** box,
    enter !\![**Contoso MFA Policy**](urn:gd:lg:a:send-vm-keys)!!.

7.  Under **Assignments**, select **0 users or workload identities
    selected**.

> ![A screenshot of a computer Description automatically
> generated](./media/image37.png)

8.  In the Users and groups pane, select the option next to **Select
    users and groups** and then select the check box next to **Users and
    groups**.

9.  On the **Select** page, select **Alex Wilber** and then
    click **Select**.

> ![A screenshot of a computer Description automatically
> generated](./media/image38.png)
>
> Note that typically you would specify a group, however for this
> exercise we will just test the setting on Alex Wilber.

10. Select **No target resources selected** under Target resources and
    then click **Select apps**.

> ![A screenshot of a computer Description automatically
> generated](./media/image39.png)

11. On the **Select** page, select the check box next to **Office
    365** and then click **Select**.

> ![A screenshot of a computer Description automatically
> generated](./media/image40.png)

12. Under **Access controls**, in the **Grant** section, select **0
    controls selected**.

> ![A screenshot of a computer Description automatically
> generated](./media/image41.png)

13. On the **Grant** page, select **Grant access**, select the check box
    next to **Require multi-factor authentication**, and then
    click **Select**.

> ![A screenshot of a computer Description automatically
> generated](./media/image42.png)

14. Under **Enable policy**, select **On**.

15. Select **Create** to create the Contoso MFA Policy. Notice that the
    policy is listed with a State of **On**.

> ![A screenshot of a computer Description automatically
> generated](./media/image43.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image44.png)

16. In the **Microsoft Entra admin center**, select **Users**. In the
    User list, select **Alex Wilber**.

> ![A screenshot of a computer Description automatically
> generated](./media/image45.png)

17. On the Alex Wilber page, select **Authentication methods**.

> ![](./media/image46.png)
>
> Notice that a phone number has already been configured for Alex,

18. Close Microsoft Edge.

Task 3: Validate conditional access MFA

1.  Switch to [**SEA-WS3**](urn:gd:lg:a:select-vm). On the taskbar,
    select **Microsoft Edge**.

2.  In the address bar,
    enter !\![**outlook.office.com**](urn:gd:lg:a:send-vm-keys)!!  and
    press Enter.

3.  On the **Pick an account** page, select
    !!**AlexW@M365xXXXXXXX.onmicrosoft.com**!!

> ![A screenshot of a computer Description automatically
> generated](./media/image12.png)

4.  On the **Enter password** page, enter !!**P@55w.rd1234**!! and
    select **Sign in**.

5.  At the **Verify your identity** prompt, select your Text phone
    number.

> ![A screenshot of a computer error Description automatically
> generated](./media/image22.png)

6.  At the **Enter code** page, enter the code sent to your mobile
    phone, and then select **Verify**.

> ![A screenshot of a computer error message Description automatically
> generated](./media/image23.png)
>
> Notice that you can select a check box to not ask for verification
> again for 30 days.

7.  At the Stay signed in message, select **No**. Outlook on the Web
    opens to Alex Wilber's inbox.

> ![A screenshot of a computer error Description automatically
> generated](./media/image25.png)

8.  At the top-right corner, select the **Account manager for Alex
    Wilber** and then select **Sign out**.

> ![A computer screen shot of a computer screen Description
> automatically generated](./media/image26.png)

9.  Close Microsoft Edge.

Task 4: Remove conditional access MFA

1.  Switch to [**SEA-SVR1**](urn:gd:lg:a:select-vm).
    On [**SEA-SVR1**](urn:gd:lg:a:select-vm), if necessary, sign in
    as [**Contoso\Administrator**](urn:gd:lg:a:send-vm-keys) with the
    password of  !\![**Pa55w.rd**](urn:gd:lg:a:send-vm-keys)!!  and
    close **Server Manager**.

2.  On the taskbar select **Microsoft Edge**, navigate to **Microsoft
    Entra admin center**  !!**https://Entra.Microsoft.com**!!

3.  Sign in with **Office 365 Tenant admin** credentials.

> ![A screenshot of a computer Description automatically
> generated](./media/image2.png)
>
> The **Microsoft Entra admin center** opens.

4.  In the **Microsoft Entra admin center**, in the navigation pane,
    expand **Identity**, then expand **Protection**, then **Conditional
    Access.**

> ![A screenshot of a computer Description automatically
> generated](./media/image35.png)

5.  On the **Conditional Access** page select **Policies** and then
    select **Contoso MFA Policy**.

6.  On the **Contoso MFA Policy** page, select **Delete** and then
    select **Delete**.

> ![A screenshot of a computer Description automatically
> generated](./media/image47.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image48.png)

7.  For Delete confirmation, click on the Delete button.

> ![A screenshot of a computer error Description automatically
> generated](./media/image49.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image50.png)

8.  Close Microsoft Edge.

**Results**: After completing this exercise, you will have successfully
configured multi-factor authentication by using a conditional access
policy.
