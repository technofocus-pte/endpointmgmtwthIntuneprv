# Lab 16 – Exploring Copilot in Intune (Security Copilot Integration)

### Summary

In this lab, you will explore **Microsoft Copilot in Intune**, powered by **Microsoft Security Copilot**. Copilot in Intune uses generative AI to help you analyze your Intune data, summarize device and policy configurations, troubleshoot issues, and take action.

These capabilities are built into the Intune admin center and provide intelligent assistance for endpoint management, policy creation, and troubleshooting by exploring Intune data with natural language.

### Prerequisites

Before beginning this lab, you need:

- The tenant admin account with the **Global Administrator** role. Security Copilot must be set up the first time by a Global Administrator or Security Administrator.
- An **Azure subscription** in the same tenant, where your account has the **Owner** or **Contributor** role. Security Copilot capacity is billed to this subscription.
- **SEA-WS1** enrolled in Intune, and the earlier labs completed, so that Copilot has policies, groups, and apps to report on.

> **Important:** Security Copilot capacity is billed **per hour** for as long as it exists, whether or not you use it. Complete **Exercise 4** at the end of this lab to delete the capacity and stop the charges.

### Scenario

Contoso wants to explore how AI can help endpoint administrators work more efficiently. With **Copilot in Intune**, IT admins can:

- Summarize policies
- Query device, app, and compliance data in natural language
- Troubleshoot devices
- Explore Intune data from the standalone Security Copilot experience
- Get recommendations and insights from Copilot summaries

## Exercise 1: Set Up and Access Copilot in Intune

### Task 1: Set up your Security Copilot capacity

1. On **SEA-SVR1**, open Microsoft Edge and go to the Azure portal at **https://portal.azure.com**. Sign in with the tenant admin account.

    ![](media/media/image1.png)

2. In the search bar, search for and select **Microsoft Security Compute Capacities**.

    ![](media/media/image2.png)

3. Click **+ Create**.

    ![](media/media/image3.png)

4. On the **Basics** tab, enter the following details:

    - Subscription: your Azure subscription
    - Resource group: select **Create new** and enter **Rg4Intune**
    - Capacity name: **SCC4Intune**
    - Prompt evaluation location: the location closest to you (for example, **United States**)
    - Security compute units: **1**

    ![](media/media/image4.png)

5. Select the acknowledgement check box and click **Review + create**.

    ![](media/media/image5.png)

6. Click **Create**.

    ![](media/media/image6.png)

7. When the deployment is complete, click **Finish setup in Security Copilot**.

    ![](media/media/image7.png)

8. On the Security Copilot page, click **Get started**.

    ![](media/media/image8.png)

9. Enter a workspace name such as **SCC4Intune-<your initials>**, select the same location as your capacity (for example, **United States**), and click **Continue**.

    ![](media/media/image9.png)

10. Select the **SCC4Intune** capacity that you created in the Azure portal and click **Continue**.

    ![](media/media/image10.png)

11. Review the data sharing and logging options and click **Continue** on each page.

    ![](media/media/image11.png)

    ![](media/media/image12.png)

    ![](media/media/image13.png)

12. On the **Assign roles** page, click **Continue**.

    ![](media/media/image14.png)

13. Click **Finish**.

    ![](media/media/image15.png)

    ![](media/media/image16.png)

### Task 2: Open Copilot in Intune

1. Open a new tab, sign in to the **Microsoft Intune admin center** (**https://intune.microsoft.com**), and select **Copilot** at the top of the page.

    ![](media/media/image17.png)

    > **Note:** If Copilot is not available yet, wait a few minutes after finishing the Security Copilot setup, and then refresh the page.

2. Verify that Copilot loads with:

    - The chat panel
    - Suggested prompts

    ![](media/media/image18.png)

## Exercise 2: Explore Copilot Chat in Intune

### Task 1: Ask general environment questions

1. In the Copilot chat panel, enter the following prompt:

    ```text
    Summarize my current Intune device compliance posture.
    ```

    ![](media/media/image19.png)

2. Review Copilot's response and its references.

    ![](media/media/image20.png)

3. Enter the following prompt to see which devices need updates:

    ```text
    Show me devices that need updates.
    ```

    ![](media/media/image21.png)

    Copilot uses Intune data to provide summaries, insights, and recommended actions based on the results.

### Task 2: Use Copilot to understand an existing policy

1. Go to **Devices → Configuration**, and select the **Contoso Developer - standard** profile from Lab 6.

2. On the profile page, select **Summarize with Copilot**.

    ![](media/media/image22.png)

3. Review the summary. Copilot generates:

    - A human-readable explanation of the policy
    - Key security details
    - Suggested improvements

    ![](media/media/image23.png)

    ![](media/media/image24.png)

    > **Note:** If Copilot returns an error about capacity, you have used up the available security compute units for this hour. In the Azure portal, open the **SCC4Intune** capacity and increase the number of **security compute units**, or wait until the next hour and try again.

    ![](media/media/image25.png)

    ![](media/media/image26.png)

## Exercise 3: Explore the Standalone Security Copilot Experience

### Task 1: Explore Intune data using Security Copilot

1. In Microsoft Edge, go to **https://securitycopilot.microsoft.com**.

2. In the prompt bar, select the **Sources** icon and ensure that the **Microsoft Intune** plugin is turned **On**.

3. Enter the following prompt to get information about the groups and apps in Intune:

    ```text
    Show me all Intune groups and all Intune apps in my tenant. For each group, list the name, type (Security/M365), membership type (Assigned/Dynamic), member count, and what Intune assignments are using that group.
    ```

    ![](media/media/image27.png)

    ![](media/media/image28.png)

    Notice that the response includes the groups and apps you created in earlier labs, such as **Contoso Developer devices** and **7-Zip**.

4. Security Copilot also suggests follow-up prompts. Select the suggested prompt that shows the apps installed on **SEA-WS1**.

    ![](media/media/image29.png)

5. Review the response.

    ![](media/media/image30.png)

    > **Note:** The response depends on which earlier labs you completed. If you completed Lab 12, **7-Zip** appears in the list. If no apps have been deployed to SEA-WS1, Copilot reports that no apps are installed.

## Exercise 4: Clean up the Security Copilot capacity

### Task 1: Delete the capacity to stop charges

1. In the Azure portal, search for and select **Resource groups**.

2. Select the **Rg4Intune** resource group, and then select **Delete resource group**.

3. Enter **Rg4Intune** to confirm, and then select **Delete**.

    > **Note:** Deleting the capacity stops the hourly charges. Copilot in Intune and Security Copilot stop working until a new capacity is created.

### Results

After completing this lab, you will have:

- Set up Security Copilot capacity and enabled Copilot in Intune
- Used Copilot chat to analyze Intune compliance, updates, and devices
- Summarized an existing configuration policy with Copilot
- Queried Intune data from the standalone Security Copilot experience
- Deleted the Security Copilot capacity to stop charges

With these capabilities, Contoso administrators can leverage AI to reduce troubleshooting time and improve decision-making.
