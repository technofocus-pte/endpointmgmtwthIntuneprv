# Lab 5 – Integrate Microsoft Defender for Endpoint with Microsoft Intune

**Summary**

In this lab, you will integrate **Microsoft Defender for Endpoint
(MDE)** with **Microsoft Intune** to enable advanced security
capabilities such as device risk scoring, endpoint detection and
response (EDR), automated investigations, and Intune compliance actions
based on device risk level. You will configure the integration, onboard
a Windows 11 device (SEA‑WS1), validate MDE sensor connectivity, and
test device risk-based conditional access.

------------------------------------------------------------------------

**Prerequisites**

Before starting this lab, ensure the following labs are completed:

- Lab 1 – Set up Microsoft Intune

- Lab 2 – Manage Microsoft Entra Device Registration

- Lab 3 – Configure and Manage Device Enrollment

- Lab 4 – Enroll Devices into Microsoft Intune

You also need:

- A valid **Microsoft Defender for Endpoint P2** or **Microsoft 365 E5
  Security** license (provided in the tenant).

- A Windows 11 device: **SEA‑WS1**, enrolled in Intune as a standard
  user (Cindy White).

------------------------------------------------------------------------

**Exercise 1: Enable Microsoft Defender for Endpoint Integration**

**Scenario**

Contoso wants to enhance endpoint protection by integrating MDE with
Intune. This enables advanced feature sets including:

- Device risk evaluation

- MDE security recommendations

- Automated remediation

- Intune compliance actions based on risk

------------------------------------------------------------------------

## Task 1: Assign Security Administrator role

## Task 1: Enable MDE Integration in Intune

1.  Sign in to the **Microsoft Intune admin center**.

2.  In the left navigation pane, select **Endpoint security**.

> ![](media/media/image1.png)

3.  Under **Setup** select **Microsoft Defender for Endpoint**.

> ![](media/media/image2.png)
>
> **Note**: Notice that the connection status is unavailable.
>
> ![](media/media/image3.png)

4.  Go to **Microsoft Defender portal**: https://security.microsoft.com

5.  Navigate to:  
    **Settings → Endpoints**

> ![](media/media/image4.png)

6.  Select **Advanced features**.

7.  Turn on the following features and click **Save preferences**

    - **Microsoft Intune connection**

    - **Endpoint protection**, **EDR**, etc.

> ![](media/media/image5.png)
>
> ![](media/media/image6.png)

8.  Click **Save Preferences**.

9.  Return to the Intune admin center and navigate to **Endpoint
    security** → **Microsoft Defender for Endpoint.** Notice that
    Connection status is now changed to **Available.**

> ![](media/media/image7.png)

10. Under **Connectors**, click **Open the connector page**.

11. Enable the following settings:

    - **Allow Microsoft Defender for Endpoint to enforce compliance** →
      *On*

    - **Connect Windows devices version 10 or later** → *On*

    - **Connect iOS and Android devices** → *On*

> ![](media/media/image8.png)

12. Click **Save**.

> ![](media/media/image9.png)

# Exercise 2: Configure Device Onboarding for Windows

**Scenario**

To onboard Windows devices into Defender for Endpoint, Contoso will use
Intune's built‑in onboarding profile. Devices receive MDE sensor
settings automatically upon assignment.

------------------------------------------------------------------------

## Task 1: Create an MDE Onboarding Policy in Intune

1.  In Intune, select **Endpoint security**, select **Endpoint detection
    and response**.

> ![](media/media/image10.png)

2.  Scroll down the page and click **+ Create Policy**.

> ![](media/media/image11.png)

3.  Select the following and click **Create**

    - **Platform:** Windows

    - **Profile:** Endpoint detection and response

> ![](media/media/image12.png)

4.  On the **Basics** tab enter the following details and click
    **Next**.

- Name: **Contoso – MDE Onboarding Policy**

- Description: **Onboards Windows devices into Microsoft Defender for
  Endpoint**

> ![](media/media/image13.png)

5.  **On the Configuration Settings blade select the following for
    Microsoft Defender for Endpoint**

- Microsoft Defender for Endpoint client configuration package type 🡪
  select Auto from connector

- **Sample sharing diagnostic** →All

Click **Next**.

> ![](media/media/image14.png)

6.  On the **Scopes** tab click **Next**, on the **Assignments** tab
    select **Contoso Developer devices.** Click **Next** → **Save**.

![](media/media/image15.png)

![](media/media/image16.png)

------------------------------------------------------------------------

# Exercise 3: Sync and Validate MDE Onboarding on SEA‑WS1

## Task 1: Sync the Device

1.  On **SEA‑WS1**, sign in as **Cindy White**.

2.  Open **Settings → Accounts → Access work or school**.

> ![](media/media/image17.png)

3.  Select **Connected to Contoso’s Azure AD** → **Info**.

> ![](media/media/image18.png)

4.  Scroll down and select **Sync**.

> ![](media/media/image19.png)

*Note: It may take 5–10 minutes for the onboarding to complete.*

5.  On SEA‑WS1, open **Terminal admin)**.

![](media/media/image20.png)

7.  Run:

> sc query sense
>
> ![](media/media/image21.png)

8.  Open **Windows Security** → **Virus & threat protection**.

> ![](media/media/image22.png)

9.  Confirm the following features are **On** by default.

    - Real-time protection: **On**

    - Cloud-delivered protection: **On**

> ![](media/media/image23.png)

10. Back on SEA-SVR1, go to **security.microsoft.com**

11. Navigate to:  
    **Assets → Devices**

> ![](media/media/image24.png)

12. Ensure that **SEA‑WS1** is listed

13. Confirm:

    - Device is listed

    - MDE sensor active

    - "Onboarded" status is **Active**

> ![](media/media/image25.png)

------------------------------------------------------------------------

# Exercise 4: Configure Intune Compliance Based on Device Risk

**Scenario**

Contoso wants to block access if a device is considered "High Risk" by
Defender for Endpoint. This ensures compromised devices cannot access
corporate resources.

------------------------------------------------------------------------

## Task 1: Create a Device Compliance Policy Based on MDE

1.  In Intune, select **Devices → Compliance policies**.

> ![](media/media/image26.png)

2.  Click **+ Create policy**.

> ![](media/media/image27.png)

3.  Select:

    - Platform: **Windows 10 and later**

    - Profile type: **Template**

    - Select **Microsoft Defender for Endpoint**.

> ![](media/media/image28.png)

4.  Click Create**.**

5.  On the **Basics** tab enter the following policy name

Name: **Contoso Developer – Device risk policy  
**![](media/media/image29.png)

6.  On the Configurations tab configure the following and click
    **Next**.

Sample sharing for all files: **Block**

Expedite telemetry reporting frequency: **Enable**

![](media/media/image30.png)

7.  On the **Assignments** page Assign to: **Contoso Developer devices**
    and Click Next → Create.

![](media/media/image31.png)

![](media/media/image32.png)

![](media/media/image33.png)

------------------------------------------------------------------------

**Results**

After completing this lab, you have successfully:

- Integrated **Microsoft Defender for Endpoint** with Intune

- Onboarded a Windows 11 device into Defender

- Enabled EDR, cloud-delivered protection, and sensor monitoring

- Configured Intune to enforce compliance based on device risk

Your Contoso environment now has full **endpoint protection**, **device
risk evaluation**, and **conditional access enforcement**.

------------------------------------------------------------------------
