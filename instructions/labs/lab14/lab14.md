Lab14 - Deploy Apps using Endpoint Configuration Manager

**Summary**

In this lab, you will use Microsoft Endpoint Configuration Manager to
deploy applications to desktop client workstations.

**Scenario**

Contoso uses Microsoft Endpoint Configuration Manager to manage desktop
workstations within the on-premises Active Directory network
environment. You need to deploy a new application named Microsoft Power
BI desktop to the Windows 11 Configuration Manager clients. The Endpoint
Configuration Manager administrator has already created the application
object for you. Your tasks include creating a collection for the target
devices, distributing the application content to distribution points,
and then creating the deployment assigned to the target collection. You
will verify the process by ensuring that the application is displayed in
the Software Center on SEA-CL1.

Task 1: Create a device collection

1.  Switch to [***SEA-CFG1***](urn:gd:lg:a:select-vm), sign in
    as [**Contoso\Administrator**](urn:gd:lg:a:send-vm-keys) with the
    password !\![**Pa55w.rd**](urn:gd:lg:a:send-vm-keys)!!.

2.  On the taskbar, select **Configuration Manager Console**. The
    Microsoft Endpoint Configuration Manager console opens.

> ![](./media/image1.png)

3.  In the **Assets and Compliance** workspace, select **Device
    Collections**.

> ![A screenshot of a computer Description automatically
> generated](./media/image2.png)

4.  Right-click **Device Collections** and then select **Create Device
    Collection**. The Create Device Collection Wizard opens.

> ![A screenshot of a computer Description automatically
> generated](./media/image3.png)

5.  On the **General** page, configure the following and then
    select **Next**:

    - Name: !\![**Power BI App Deployment**](urn:gd:lg:a:send-vm-keys)!!

    - Comment: !\![**Devices targeted to install Power BI
      Desktop**](urn:gd:lg:a:send-vm-keys)!!

    - Limiting collection: **All Windows 11 Workstations**

> ![A screenshot of a computer Description automatically
> generated](./media/image4.png)

6.  On the **Membership Rules** page, select **Next**. At the
    Configuration Manager warning, select **OK**. You will add a direct
    member at a later step.

> ![A screenshot of a computer Description automatically
> generated](./media/image5.png)
>
> ![A screenshot of a computer error Description automatically
> generated](./media/image6.png)

7.  On the **Summary** page, select **Next** and then on
    the **Completion** page, select **Close**.

> ![A screenshot of a computer Description automatically
> generated](./media/image7.png)
>
> The **Power BI App Deployment** collection is displayed in the Device
> Collections list.
>
> ![A screenshot of a computer Description automatically
> generated](./media/image8.png)

Task 2: Assign a Device to an existing Collection

1.  In the **Assets and Compliance** workspace, select **Devices**.

> Take note of the devices listed. Any device that has a green circle
> with a white checkmark are currently active.
>
> ![](./media/image9.png)

2.  In the details pane, select **SEA-CL1**.

3.  Right-click [***SEA-CL1***](urn:gd:lg:a:select-vm), point to **Add
    Selected Items**, and then select **Add Selected Items to Existing
    Device Collection**.

> ![](./media/image10.png)

4.  On the **Select Collection** dialog box, select **Power BI App
    Deployment**, and then select **OK**.

> ![A screenshot of a computer Description automatically
> generated](./media/image11.png)

5.  To verify, in the **Assets and Compliance** workspace,
    select **Device Collections** and then double-click **Power BI App
    Deployment**.

> ![A screenshot of a computer Description automatically
> generated](./media/image12.png)
>
> [***SEA-CL1***](urn:gd:lg:a:select-vm) should be listed as a member of
> this collection.
>
> ![A screenshot of a computer Description automatically
> generated](./media/image13.png)

Task 3: Configure a deployment type

1.  In the Microsoft Endpoint Configuration Manager console select
    the **Software Library** workspace.

> ![A screenshot of a software library Description automatically
> generated](./media/image14.png)

2.  In the **Software Library** workspace, expand **Application
    Management** and then select **Applications**.

> ![A screenshot of a software library Description automatically
> generated](./media/image15.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image16.png)
>
> Notice the applications that have been created by the Endpoint
> Configuration Manager administrator.

3.  In the details pane, select **Microsoft Power BI Desktop (x64)**.

> ![A screenshot of a computer Description automatically
> generated](./media/image17.png)

4.  In the results pane, select the **Deployment Types** tab. Notice
    that there is one deployment type that is based upon Windows
    Installer.

> ![A screenshot of a computer Description automatically
> generated](./media/image18.png)

5.  Right-click the **Microsoft Power BI Desktop (x64) - Windows
    installer** deployment type and then select **Properties**.

> ![A screenshot of a computer Description automatically
> generated](./media/image19.png)

6.  In the **Properties** dialog box, select the **Programs** tab. Take
    note of how the application is installed. It will use msiexec with
    the /q switch which performs a quiet installation.

> ![](./media/image20.png)

7.  In the **Properties** dialog box, select the **Requirements** tab
    and then select **Add**.

> ![A screenshot of a computer Description automatically
> generated](./media/image21.png)

8.  In the **Create Requirement** dialog box, configure the following
    and then select **OK**:

    - Category: **Device**

    - Condition: **Operating System**

    - Rule type: **Value**

    - Operator: **One of Windows 11 (Select the check box next to
      Windows 11)**

> ![A screenshot of a computer program Description automatically
> generated](./media/image22.png)

9.  In the **Properties** dialog box, select **OK**. This requirement
    will prevent the app from installing on any operating system except
    Windows 11.

> ![A screenshot of a computer Description automatically
> generated](./media/image23.png)

Task 4: Distribute content to distribution points

1.  In the **Software Library** workspace, select **Microsoft Power BI
    Desktop (x64)**.

2.  Right-click **Microsoft Power BI Desktop (x64)** and then
    select **Distribute Content**.

> ![A screenshot of a computer Description automatically
> generated](./media/image24.png)

3.  On the **General** page, select **Next**.

> ![A screenshot of a computer Description automatically
> generated](./media/image25.png)

4.  On the **Content** page, select **Next**.

> ![A screenshot of a computer Description automatically
> generated](./media/image26.png)

5.  On the **Content Destination** page, select **Add** and then
    select **Distribution Point**.

> ![A screenshot of a computer Description automatically
> generated](./media/image27.png)

6.  On the **Add Distribution Points** dialog box, select the check box
    next to **SEA-CFG1.CONTOSO.COM**, and then select **OK**.

> ![A screenshot of a computer Description automatically
> generated](./media/image28.png)

7.  On the **Content Destination** page, select **Next**.

> ![A screenshot of a computer Description automatically
> generated](./media/image29.png)

8.  On the **Summary** page, select **Next** and then select **Close**.

> ![A screenshot of a computer Description automatically
> generated](./media/image30.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image31.png)

9.  In the **Summary** tab, select **Content Status**.

> ![A screenshot of a computer Description automatically
> generated](./media/image32.png)
>
> The Content Status page opens for Microsoft Power BI Desktop. In the
> results pane, verify that a green circle is displayed and that
> Success:1 displays next to the circle. This indicates that the content
> is now distributed to the distribution points and can now be deployed
> to devices. You may need to select the Refresh button in the ribbon.
>
> ![A screenshot of a computer Description automatically
> generated](./media/image33.png)

10. In the top left corner select the **Back to Applications** arrow to
    return to the Software Library Applications node.

Task 5: Create a deployment

1.  In the **Software Library** workspace, select **Microsoft Power BI
    Desktop (x64)**.

2.  Right-click **Microsoft Power BI Desktop (x64)** and then
    select **Deploy**. The **Deploy Software Wizard** opens.

> ![A screenshot of a computer Description automatically
> generated](./media/image34.png)

3.  On the **General** page, next to **Collection**, select **Browse**.

> ![A screenshot of a computer Description automatically
> generated](./media/image35.png)

4.  On the **Select Collection** page, select **User Collections** and
    then select **Device Collections**.

5.  In the **Device Collections** list, select **Power BI App
    Deployment** and then select **OK**.

> ![A screenshot of a computer Description automatically
> generated](./media/image36.png)

6.  On the **General** page, select **Next**.

> ![A screenshot of a computer Description automatically
> generated](./media/image37.png)

7.  On the **Content** page, select **Next**.

> ![A screenshot of a computer Description automatically
> generated](./media/image38.png)

8.  On the **Deployment Settings** page, verify that the **Action** is
    set to **Install** and the **Purpose** is set to **Available**.
    Select **Next**.

> ![A screenshot of a computer Description automatically
> generated](./media/image39.png)

9.  On the **Scheduling** page, select **Next**. The application will be
    available as soon as possible by default.

> ![A screenshot of a computer Description automatically
> generated](./media/image40.png)

10. On the **User Experience** page, next to **User notifications**,
    select **Display in Software Center and show all notifications**.
    Select **Next**.

> ![A screenshot of a computer Description automatically
> generated](./media/image41.png)

11. On the **Alerts** page, select **Next**.

> ![A screenshot of a computer Description automatically
> generated](./media/image42.png)

12. On the **Summary** page, select **Next** and then select **Close**.

> ![A screenshot of a computer Description automatically
> generated](./media/image43.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image44.png)

13. In the results pane, on the **Deployments** tab, verify that the
    deployment displays.

> ![A screenshot of a computer Description automatically
> generated](./media/image45.png)

14. Close the Microsoft Endpoint Configuration Manager console.

15. Sign out of [***SEA-CFG1***](urn:gd:lg:a:select-vm).

Task 6: Use Software center to install a deployed app

1.  Switch to [***SEA-CL1***](urn:gd:lg:a:select-vm), and sign in
    as [**Contoso\Administrator**](urn:gd:lg:a:send-vm-keys) with the
    password of !\![**Pa55w.rd**](urn:gd:lg:a:send-vm-keys)!!.

2.  Click on the **Start Menu** and then enter **Control Panel**.

3.  In the results, select **Control Panel**.

> ![A screenshot of a computer Description automatically
> generated](./media/image46.png)

4.  In the **Control panel**, select **System and Security**.

> ![A screenshot of a computer Description automatically
> generated](./media/image47.png)

5.  In **System and Security**, select **Configuration Manager**.
    Configuration Manager Properties is displayed.

> ![A screenshot of a computer Description automatically
> generated](./media/image48.png)

6.  In the **Configuration Manager Properties** dialog box, select
    the **Actions** tab.

> ![A screenshot of a computer program Description automatically
> generated](./media/image49.png)

7.  On the **Actions** tab, select **Machine Policy Retrieval &
    Evaluation Cycle**, and then select **Run Now**. At the message
    prompt, select **OK**.

> ![A screenshot of a computer program Description automatically
> generated](./media/image50.png)
>
> ![A screenshot of a computer Description automatically
> generated](./media/image51.png)

8.  Select **OK** to close the **Configuration Manager Properties**, and
    then close **Control Panel**.

> ![A screenshot of a computer program Description automatically
> generated](./media/image52.png)

9.  In the notification area, select **New Software is Available** and
    then select **Open Software Center**. You might need to expand the
    notification area arrow to display the icon.

> ![](./media/image53.png)
>
> If the Software Center does not launch, then click on the **Start
> Menu** and scroll down and click on !!**Software Center**!!
>
> ![A screenshot of a computer Description automatically
> generated](./media/image54.png)

10. In the **Software Center**, on the **Applications** page, notice the
    new application available named **Microsoft Power BI Desktop
    (x64)**. This application is now available to any device that is a
    member of the **Power BI App Deployment** collection created
    previously.

> ![A screenshot of a computer Description automatically
> generated](./media/image55.png)

11. Select **Microsoft Power BI Desktop (x64)** and then
    select **Install**.

> ![A screenshot of a computer Description automatically
> generated](./media/image56.png)
>
> ![](./media/image57.png)
>
> The application downloads and installs without user input. You will
> know that the installation was successful when the **Power BI
> Desktop** shortcut displays on the desktop.
>
> ![A screenshot of a computer Description automatically
> generated](./media/image58.png)

12. Close Software Center.

13. Sign out of [***SEA-CL1***](urn:gd:lg:a:select-vm).

**Results**: After completing this exercise, you will have successfully
used Microsoft Endpoint Configuration Manager to deploy applications to
desktop client workstations.
