# Lab 16 – Exploring Copilot in Intune (Security Copilot Integration)

**Summary**

In this lab, you will explore **Microsoft Copilot in Intune**, powered
by **Microsoft Security Copilot**. Copilot in Intune uses generative AI
to help you analyze your Intune data, summarize device and policy
configurations, troubleshoot issues, and take action

These capabilities are built into the Intune admin center and provide
intelligent assistance for endpoint management, policy creation, and
troubleshooting.  
Microsoft states that Copilot in Intune helps manage policies and
settings, understand security posture, and troubleshoot device issues by
exploring Intune data with natural language.

------------------------------------------------------------------------

**Prerequisites**

Before beginning this lab:

- You must have one of these roles:

  - Global Administrator

  - Intune Administrator

  - A Security Copilot role granting Intune access

- At least **one enrolled Windows 11 device** (SEA‑WS1)

- Intune tenant with Copilot enabled:

  - Intune admin center → **Tenant administration → Copilot** (verify
    status)
    [\[learn.microsoft.com\]](https://learn.microsoft.com/en-us/entra/identity/users/users-bulk-download)

------------------------------------------------------------------------

**Scenario**

Contoso wants to explore how AI can help endpoint administrators work
more efficiently. With **Copilot in Intune**, IT admins can:

- Summarize policies

- Query device/app/compliance data in natural language

- Troubleshoot devices

- Create groups and take action directly from results

- Explore Intune data via the **Explorer** interface

- Get recommendations and insights from Copilot summaries

Microsoft’s documentation confirms that Copilot in Intune allows admins
to “explore Intune data, troubleshoot issues, manage settings, and take
action using natural language,” including the new Explorer experience
that queries Intune’s data platform.
[\[github.com\]](https://github.com/MicrosoftDocs/entra-docs/blob/main/docs/identity/users/users-bulk-download.md)

------------------------------------------------------------------------

## Exercise 1: Access Copilot in Intune

### Task 1: Set up your Copilot capacity.

1.  Navigate to Azure portal following the URL
    <https://portal.azure.com>

![](media/media/image1.png)

2.  On the Azure portal on the search bar, search for **Microsoft
    Security compute capacities**

![](media/media/image2.png)

3.  Click Create to create **SCC’s**.

![](media/media/image3.png)

4.  On the basics tab enter the following details

Resource group create new: **Rg4Intune**

Capacity name : **SCC4Intune**

![](media/media/image4.png)

5.  Click on the checkbox for acknowledgement and click Review+Create

![](media/media/image5.png)

6.  Click Create.

![](media/media/image6.png)

7.  Once the Secure compute capacities are deployed click on the
    **Finish setup in Security Copilot.**

![](media/media/image7.png)

8.  On the Security Copilot page click on **Get Started.**

![](media/media/image8.png)

9.  Enter Workspace name as **SCC4Intune2702,** select location as
    **United states** and click **Continue.**

![](media/media/image9.png)

10. Select the capacity that we have created in the Azure portal and
    click Continue.

![](media/media/image10.png)

11. Click Continue

![](media/media/image11.png)

![](media/media/image12.png)

![](media/media/image13.png)

12. Click Continue on the assign roles page

![](media/media/image14.png)

13. Click **Finish**

![](media/media/image15.png)

![](media/media/image16.png)

### Task 2: Open Copilot

1.  Sign in to the **Microsoft Intune admin center**. select
    **Copilot**.

> ![](media/media/image17.png)

2.  Verify that Copilot loads with:

    - Chat panel

    - Suggested prompts

    - Explorer option (if enabled)

> ![](media/media/image18.png)

------------------------------------------------------------------------

## Exercise 2: Explore Copilot Chat in Intune

### Task 1: Ask General Environment Questions

1.  In the Copilot chat panel, enter the following prompt:

- **“Summarize my current Intune device compliance posture.”**

> ![](media/media/image19.png)

2.  Copilot will respond with references.

![](media/media/image20.png)

3.  Now lets run the following prompt to know about the devices that
    will need updates

- **“Show me devices that need updates.”**

> ![](media/media/image21.png)

Copilot uses Intune data to provide summaries, insights, and recommended
actions based on results

------------------------------------------------------------------------

### Task 2: Use Copilot to Understand an Existing Policy

1.  Go to **Devices → Configuration profiles**.

2.  Click **Copilot → Summarize policy**.

> ![](media/media/image22.png)

Copilot will generate:

- A human-readable explanation

- Key security details

- Suggested improvements (as per the Copilot in Intune feature overview)

> ![](media/media/image23.png)
>
> ![](media/media/image24.png)
>
> **Note**: if copilot throws error about capacity, we will need to
> increase the Secure compute capacity
>
> ![](media/media/image25.png)
>
> ![](media/media/image26.png)

------------------------------------------------------------------------

## Exercise 3: Explore the Copilot “stand alone” Experience

------------------------------------------------------------------------

### Task 1: Exploring Intune Data Using Security Copilot

1.  Navigate to Microsoft Security Copilot page.

2.  Enter the following prompt to get information on all the groups and
    devices enrolled in Intune.

> **Show me all Intune groups and all Intune apps in my tenant. For each
> group, list the name, type (Security/M365), membership type
> (Assigned/Dynamic), member count, and what Intune assignments are
> using that group.**
>
> ![](media/media/image27.png)
>
> ![](media/media/image27.png)
>
> ![](media/media/image28.png)

3.  Security Copilot also suggests prompts, select any of those
    prompts.  
    here we have selected the prompt to see the apps installed on
    SEA-WS1 virtual machine.

> ![](media/media/image29.png)

4.  Since there are no apps installed on the VM copilot has responded
    the same.

> ![](media/media/image30.png)

### Summary

> After completing this lab, you have:

- Explored and enabled Copilot in Intune

- Used Copilot chat to analyze Intune settings, compliance, and devices

- Learned how Security Copilot enhances intelligence and insight within
  Intune

> With these capabilities, Contoso administrators can now leverage AI to
> dramatically reduce troubleshooting time and improve decision-making.
