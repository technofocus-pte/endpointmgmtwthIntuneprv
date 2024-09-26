Lab 21: Refreshing Windows with Autopilot Reset and Self-Deploying mode.

**Summary**

In this lab you will learn how perform a remote Autopilot reset.

**Prerequisites**

To following lab(s) must be completed before this lab:

-   Lab 01-Managing Identities in Microsoft Entra ID

-   Lab 02-Synchronizing Identities by using Azure AD Connect

-   Lab 21-Deploying Windows 11 using Microsoft Deployment Toolkit

-   Lab 20-Deploying Windows 11 with Autopilot

**Scenario**

SEA-WS4 has been deployed by using Windows Autopilot. You need to test
out another provisioning scenario that involves Autopilot Reset. You
will create a new deployment profile configured with the Windows
Autopilot Self-Deploying mode.

Task 1: Configure a Self-Deploying Windows Autopilot deployment profile

1.  Switch to [**[SEA-SVR1]{.underline}**](urn:gd:lg:a:select-vm).

> ![](./media/image1.png){width="6.5in" height="4.379166666666666in"}

2.  In **Microsoft Edge**, open a new tab and navigate
    to [**https://intune.microsoft.com**](https://intune.microsoft.com).
    If prompted, sign in
    with [**admin@M365xXXXXXXXX.onmicrosoft.com**](mailto:admin@M365xXXXXXXXX.onmicrosoft.com) and paswword.

3.  In the **Microsoft Intune admin center**, select **Devices**.

> ![A screenshot of a computer Description automatically
> generated](./media/image2.png){width="6.108251312335958in"
> height="4.304962817147857in"}

4.  In the **Device onboarding** section, select **Enrollment**.

> ![A screenshot of a computer Description automatically
> generated](./media/image3.png){width="4.159031058617673in"
> height="4.555130139982502in"}

5.  On the Windows enrollment blade, in the details pane,
    select **Deployment Profiles**.

> ![](./media/image4.png){width="6.5in" height="3.7131944444444445in"}

6.  On the **Windows AutoPilot deployment profiles** blade,
    select **Contoso Profile 1** and then select **Properties**.

> ![](./media/image5.png){width="6.5in" height="3.1166666666666667in"}
>
> ![A screenshot of a computer Description automatically
> generated](./media/image6.png){width="6.097828083989501in"
> height="3.68996719160105in"}
>
> ![A screenshot of a computer Description automatically
> generated](./media/image7.png){width="3.8046281714785652in"
> height="3.5336132983377078in"}

7.  Scroll down to **Assignments** and then select **Edit**.

> ![A screenshot of a computer Description automatically
> generated](./media/image8.png){width="6.045709755030622in"
> height="4.48216426071741in"}

8.  Next to **IT Devices**, select **Remove**.

> ![](./media/image9.png){width="6.5in" height="4.313194444444444in"}

9.  Select **Review and save** and then select **Save**.

> ![A screenshot of a computer Description automatically
> generated](./media/image10.png){width="4.086066272965879in"
> height="4.461316710411198in"}

10. Close the **Contoso Profile 1\|Properties** page.

11. On the **Windows AutoPilot deployment profiles** blade,
    select **Create profile** and then select **Windows PC**.

> ![A screenshot of a computer Description automatically
> generated](./media/image11.png){width="6.5in" height="3.49375in"}

12. In the **Basics** tab, in the **Name** text box, type [**Contoso
    profile 2**](urn:gd:lg:a:send-vm-keys).

13. For **Convert all targeted devices to Autopilot** select **No**, and
    then select **Next**.

> ![](./media/image12.png){width="6.076980533683289in"
> height="4.440469160104987in"}

14. On the **Out-of-box experience (OOBE)** tab, ensure that
    the **Deployment mode** is set to **Self-Deploying**.

> ![](./media/image13.png){width="6.5in" height="3.9340277777777777in"}

15. Ensure that the following options are set:

    -   Language (Region): **Operating system default**

    -   Automatically configure keyboard: **Yes**

    -   Apply device name template: **Yes**

    -   Enter a name: [**Contoso-%RAND:2%**](urn:gd:lg:a:send-vm-keys)

> ![A screenshot of a computer Description automatically
> generated](./media/image14.png){width="6.5in"
> height="3.3201388888888888in"}

16. Select **Next**.

17. On the **Assignments** tab, under **Included groups** select **Add
    groups**.

> ![A screenshot of a computer Description automatically
> generated](./media/image15.png){width="6.5in"
> height="3.7333333333333334in"}

18. Select the **IT Devices** group and click **Select**.
    Select **Next**.

> ![](./media/image16.png){width="5.691305774278216in"
> height="4.815720691163604in"}
>
> ![A screenshot of a computer Description automatically
> generated](./media/image17.png){width="5.003346456692913in"
> height="4.85741469816273in"}

19. On the **Review + create** blade, review the information and then
    select **Create**.

> ![A screenshot of a computer Description automatically
> generated](./media/image18.png){width="5.59749343832021in"
> height="4.9303805774278215in"}

Task 2: Perform an Autopilot reset

1.  In the **Microsoft Intune admin center**, select **Devices** and
    then select **All devices**.

2.  Select the Autopilot PC (Begins with the name DESKTOP).

> ![A screenshot of a computer Description automatically
> generated](./media/image19.png){width="6.5in"
> height="4.143055555555556in"}

3.  In the menu bar, select the ellipse and then select **Autopilot
    Reset**.

> ![A screenshot of a computer Description automatically
> generated](./media/image20.png){width="6.5in"
> height="3.9368055555555554in"}

4.  At the message prompt, select **Yes**.

> ![A screenshot of a computer Description automatically
> generated](./media/image21.png){width="5.1388538932633425in"
> height="1.6052405949256343in"}

5.  Switch to [**[SEA-SVR2]{.underline}**](urn:gd:lg:a:select-vm) and
    maximize the **SEA-WS4** window.

> **Note**: SEA-WS4 should still be running from the previous lab
>
> **Note**: Update the device to the latest version and then click on
> restart.

6.  Restart **SEA-WS4**.

> ![A screenshot of a computer Description automatically
> generated](./media/image22.png){width="6.5in"
> height="4.531944444444444in"}
>
> **Note**: This process can take 30 minutes and will reboot several
> times during the process. Your instructor may continue with the next
> module while this task completes. Be sure to come back to complete
> Task 3 during your next lab session.

Task 3: Verify Autopilot deployment

1.  At the sign-in page,
    enter [**Cindy@M365x19242953.onmicrosoft.com**](mailto:Cindy@M365x19242953.onmicrosoft.com) with
    the Password of  [**P@55w.rd1234**](mailto:P@55w.rd1234).

2.  At the **Use Windows Hello with your account**, select **OK**.

> ![A screenshot of a computer Description automatically
> generated](./media/image23.png){width="6.5in"
> height="4.826388888888889in"}

3.  At the **Verify your identity** page, select the Text verification
    method.

4.  At the **Enter code** page, enter the code that has been texted to
    your mobile device and then select **Verify**.

> ![A screenshot of a computer Description automatically
> generated](./media/image24.png){width="4.887391732283464in"
> height="4.762341426071741in"}

5.  On the **Setup up a PIN** dialog box, in the **New
    PIN** and **Confirm PIN** fields,
    enter [**102938**](urn:gd:lg:a:send-vm-keys), and then
    select **OK**.

> ![](./media/image25.png){width="6.5in" height="4.73125in"}

6.  On the **All set!** page, select **OK**.

7.  Select **Start** and select **Settings**.

> ![](./media/image26.png){width="4.751920384951881in"
> height="4.960337926509187in"}

8.  Select **Accounts**, and then select **Access work or school**.
    Verify the device is connected to Contoso\'s Azure AD.

> ![](./media/image27.png){width="6.5in" height="4.820138888888889in"}

9.  Select **Connected to Contoso\'s Azure AD** and select **Info**.

> ![](./media/image28.png){width="6.5in" height="4.538194444444445in"}

10. On the **Managed by Contoso** page, scroll down and then
    select **Sync**.

> ![](./media/image29.png){width="6.5in" height="4.539583333333334in"}

11. On **SEA-WS4**, close the **Settings** window.

12. Shut down **SEA-WS4** and close the **SEA-WS4** window.

13. On [**[SEA-SVR2]{.underline}**](urn:gd:lg:a:select-vm), close
    Hyper-V Manager.

**Results**: After completing this exercise, you will have provisioned a
Windows 11 device with Autopilot Reset using Self-Deploying mode.
