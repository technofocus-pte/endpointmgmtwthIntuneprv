# Lab 10 – Implement Mobile Application Management (MAM) Using App Protection Policies in Microsoft Intune

**Summary**

In this lab, you will use Microsoft Intune to configure and test
**Mobile Application Management (MAM)** for unmanaged (BYOD) mobile
devices. You will create an **App Protection Policy**, configure **MAM
Conditional Access**, deploy Microsoft 365 applications, and validate
selective wipe capabilities. This lab focuses on protecting *corporate
data within apps* without requiring full device enrollment.

------------------------------------------------------------------------

**Prerequisites**

The following labs must be completed before this lab:

- Lab 1 – Set up Microsoft Intune

- Lab 2 – Manage Microsoft Entra Device Registration

- Lab 3 – Configure and Manage Device Enrollment

- Lab 4 – Enroll Devices into Microsoft Intune

You will also need a personal Android or iOS mobile device capable of
installing apps and receiving MFA prompts.

------------------------------------------------------------------------

## Exercise 1: Create an App Protection Policy (MAM) for BYOD Devices

**Scenario**

The Contoso IT team is planning to allow employees to access Outlook,
Teams, and OneDrive on their personal phones. However, corporate data
must be protected using Intune Mobile Application Management (MAM).
Cindy White will help validate that app data is being protected under
MAM policies on her personal device.

The policy requirements are:

- Prevent saving corporate data to personal storage

- Prevent copy/paste outside corporate apps

- Require a PIN to open corporate apps

- Encrypt data at rest within the app

- Block access from jailbroken/rooted devices

------------------------------------------------------------------------

### Task 1: Create an App Protection Policy (Android)

1.  On **SEA-SVR1**, Sign in to **Microsoft Intune admin center** as an
    admin.

> ![](media/media/image1.png)

2.  In the left navigation pane, select **Apps**.

> ![](media/media/image2.png)

3.  Under Manage apps select **Protection,** then on the **Apps |
    Protection** page, click on **+ Create** and select **Android.**

> ![](media/media/image3.png)

4.  On the **Basics** page, enter:

    - Name: **Contoso MAM – Mobile App Protection**

    - Description: **App protection policy for BYOD devices.**  
      Click **Next**.

> ![](media/media/image4.png)

5.  On the Apps tab, set *Target policy to* “**All Microsoft Apps**” and
    then click **Next**.

> ![](media/media/image5.png)

6.  In the **Data protection** section, configure the following and
    click **Next.**

    - **Backup Org data to personal storage** → *Block*

    - **Send org data to other apps** → *Policy-managed apps only*

    - **Cut/Copy/Paste** → *Policy-managed apps only*

    - **Encrypt Org data** → *Require*

    - **Screen capture and Google Assistant** 🡪 Blocked

> ![](media/media/image6.png)
>
> ![](media/media/image7.png)

7.  In the **Access requirements** page, set the following and click
    **Next**

    - **PIN for access** → *Require*

    - **PIN type** → *Numeric*

    - **Biometric** → *Allow*

> ![](media/media/image8.png)

8.  On the **Conditional launch** page, under Device conditions
    configure the following and click **Next.**

    - Ensure Jailbroken or rooted devices is set to ***Block access.***

> ![](media/media/image9.png)

9.  In the **Assignments** section, under **Included groups**, select:  
    **Contoso Developer devices** and click **Next**

![](media/media/image10.png)

10. On Review + Create page click **Create**.

> ![](media/media/image11.png)

Your MAM App Protection Policy is now active.

![](media/media/image12.png)

------------------------------------------------------------------------

## Exercise 2: Configure MAM Conditional Access

**Scenario**

To ensure only protected apps can access corporate data, Contoso wants
to require users to use applications covered by the MAM policy.

------------------------------------------------------------------------

### Task 1: Create a MAM Conditional Access Policy

1.  Go to **Microsoft Entra admin center**.

> ![](media/media/image13.png)

2.  In the left menu, select **Entra ID** → **Conditional Access**.

> ![](media/media/image14.png)

3.  On the **Conditional Access | Overview** page Select **+ Create new
    policy**.

> ![](media/media/image15.png)

4.  Name the policy: **Require APP for Mobile Access**

5.  Under **Users or agents (Preview)**, select **Contoso Developer
    devices** group.

> ![](media/media/image16.png)

6.  Under Target resources click on No target resources selected and
    ensure **Resources** (formerly Cloud Apps) is selected, then click
    on the radio button to select resources  
    **Office 365** or **Microsoft 365**

> ![](media/media/image17.png)
>
> ![](media/media/image18.png)

7.  In the ***Conditions*** section, select ***Device platforms***,
    enable configuration, and choose ***Android*** as the selected
    platform.

![](media/media/image19.png)

8.  Under **Grant**, select:

    - **Require app protection policy**

> ![](media/media/image20.png)

9.  Toggle the Enable policy button to **On** and click **Create**.

> ![](media/media/image21.png)

This enforces secure access only through apps protected by your policy.

------------------------------------------------------------------------

**Exercise 3: Test MAM Policy Enforcement on Personal Device**

**What Happens When a User Signs in to a Managed App**

When a user such as **Cindy White** signs into Outlook on a personal
Android device:

- The app prompts the user to **create an application PIN** before
  accessing corporate data.

- Sensitive corporate data inside the app is **encrypted at rest**,
  ensuring separation from personal data stored on the device.

- **Copy/paste restrictions** take effect, allowing data to move only
  between approved (policy‑managed) applications.

- Users cannot save organizational data to **personal storage
  locations**, such as personal cloud apps or local device folders.

- The app may require **re-authentication** after a period of inactivity
  or when reopening the app, depending on policy settings.

These behaviors ensure that Contoso’s data remains protected even when
accessed on unmanaged personal devices.

------------------------------------------------------------------------

**Summary**

After completing this lab, you will have:

- Configured a full **Mobile Application Management (MAM)** strategy

- Created and assigned **App Protection Policies**

- Implemented **MAM Conditional Access**

- Protected corporate data on personal devices

- Ensured secure access to Outlook, Teams, and OneDrive without device
  enrollment

------------------------------------------------------------------------
