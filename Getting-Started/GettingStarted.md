# Respond to Incidents with Azure SRE Agent
### Overall Estimated Duration: 60 Minutes

## 📘 Lab Scenario
You are acting as a site reliability engineer for Contoso, whose small Azure-hosted web application has started returning intermittent HTTP 500 responses. In this lab, you will onboard Azure SRE Agent, confirm it is scoped to Contoso's lab workload, and add a team runbook so the agent can answer operational questions using Contoso's documented procedures instead of generic troubleshooting advice.

The lab is designed for a **60-minute** session. Spend the first few minutes reviewing the environment here, then complete Exercise 1 and Exercise 2.

## 📖 Lab Overview
In this lab, you will:

- Sign in to the Azure portal with your CloudLabs-provided account.
- Review a pre-created Azure App Service workload, Application Insights resource, and Log Analytics workspace.
- Open the Azure SRE Agent portal at <https://sre.azure.com>.
- Verify whether the Azure SRE Agent was created by the deployment, or create it manually in the portal if the preview ARM deployment path is unavailable in your tenant.
- Confirm the agent's Azure resource access is scoped to the lab workload resource group, keeping its visibility limited to that workload.
- Upload the staged runbook [C:\LabFiles\Runbooks\appservice-http-500-triage.md](file:///C:/LabFiles/Runbooks/appservice-http-500-triage.md) to the agent's Knowledge sources in Exercise 2.

## 🎯 Objectives
After completing this lab, you will be able to:

- Describe the Azure resources that make up the sample incident environment.
- Explain the preview status and supported-region requirements for Azure SRE Agent.
- Create or verify an Azure SRE Agent in the Azure SRE Agent portal.
- Confirm the agent's Azure resource access is scoped to a single workload resource group, limiting its visibility with least privilege.
- Add Markdown runbook knowledge to Azure SRE Agent's Knowledge sources and verify that responses cite or reference the uploaded guidance.

## ⚙️ Prerequisites
- Familiarity with the Azure portal and basic role-based access control (RBAC) concepts.
- Basic understanding of Application Insights, Log Analytics, and KQL.
- Familiarity with incident triage or on-call runbook concepts.
- An active Microsoft Azure subscription to provision and access required resources.
- A pre-provisioned Microsoft Entra ID user account with sufficient permissions to create and manage resources within the Azure subscription.

## 🏗️ Architecture
CloudLabs deploys a disposable lab environment that contains a Windows Lab VM, a small App Service workload, monitoring resources, and a staged operations runbook. The deployment also attempts to create an Azure SRE Agent resource when the preview API is available in the target tenant. If that preview resource cannot be deployed automatically, the exercises walk you through the documented portal fallback.

## 🖼️ Architecture Diagram

![](./../media/sre-agent-lab-technical.png)

## 🔍 Explanation of Components
- **Windows Lab VM**: Provides browser access, tools, helper files, and the staged runbook used throughout the lab.

- **Azure App Service web app**: Represents the application that is returning intermittent HTTP 500 responses. It is the workload the SRE Agent investigates.

- **Application Insights**: Collects application telemetry for requests, failures, dependencies, and diagnostics, and is one of the two supported telemetry connectors for Azure SRE Agent.

- **Log Analytics workspace**: Stores queryable operational data used by Application Insights and Azure Monitor, and can be connected to the agent as a KQL-queryable log source.

- **Runbook file**: Provides team-specific incident guidance for App Service HTTP 500 triage. The staged file is [C:\LabFiles\Runbooks\appservice-http-500-triage.md](file:///C:/LabFiles/Runbooks/appservice-http-500-triage.md). You upload this file to the agent's Knowledge sources in Exercise 2 so that chat responses can be grounded in team-specific guidance.

- **Azure SRE Agent**: Provides the agent experience for resource inspection, operational chat, and knowledge-grounded incident response. It may be pre-created by the deployment or created manually in Exercise 1.

## 🚀 Getting Started with the Lab

Welcome to your Respond to Incidents with Azure SRE Agent lab! We've prepared a seamless environment for you to explore and learn about Azure services. Let's begin by making the most of this experience:

## Accessing Your Lab Environment

Once you are ready to dive in, your virtual machine and this guide will be right at your fingertips within your web browser.

![](./../media/Accessing-Your-Lab-Environment.png)

## Lab Guide Zoom In/Zoom Out
To adjust the zoom level for the environment page, click the **A↕** icon located next to the timer in the lab environment.

![](./../media/gs-01.png)

## Resize the Virtual Machine View

Use the **slider (three vertical dots)** located between the **Virtual Machine** and the **Lab Guide** panes to adjust the display size, allowing you to customize the layout based on your preference.

![](./../media/zoom-n.png)

## Exploring Your Lab Resources
To get a better understanding of your lab resources and credentials, navigate to the **Environment** tab.

![](./../media/env-n-01.png)

## Utilizing the Split Window Feature
For convenience, you can open the lab guide in a separate window by selecting the **Split Window** button from the top right corner.

![](./../media/gs-05.png)

## Managing Your Virtual Machine

Feel free to start, stop, or restart your virtual machine as needed from the **Resources** tab. Your experience is in your hands!

![](./../media/gs-02.png)

## 🆘 Support Contact
The CloudLabs support team is available 24/7, 365 days a year, via email and live chat to ensure seamless assistance anytime. We offer dedicated support channels tailored specifically for learners and instructors, ensuring that all your needs are promptly and efficiently addressed.

Learner Support Contacts:

- Email Support: cloudlabs-support@spektrasystems.com
- Live Chat Support: <https://cloudlabs.ai/labs-support>

Click **Next** from the lower right corner to move on to the next page.

![](./../media/sre-13.png)

### Happy Learning!!