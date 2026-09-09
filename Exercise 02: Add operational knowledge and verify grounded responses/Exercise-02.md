# Exercise 02: Add Operational Knowledge and Verify Grounded Responses
### Estimated Duration: 25 Minutes

## 📘 Scenario
Your Azure SRE Agent can now inspect the lab workload, but it does not yet know your team's incident response procedures. In this exercise, you will upload a prepared App Service HTTP 500 triage runbook to the agent's Knowledge base, wait for it to be indexed, and verify that the agent uses that runbook when answering incident triage questions.

## 📖 Overview
You will review the local runbook staged on the Lab VM, upload it to Azure SRE Agent through **Builder > Knowledge base**, and then compare a broad troubleshooting answer with a response that is explicitly grounded in the uploaded runbook. The goal is to prove that the agent can reference team-specific guidance instead of only providing generic Azure troubleshooting advice.

## 🎯 Objectives
In this exercise, you will complete the following tasks:

- Task 1: Review the local App Service HTTP 500 runbook
- Task 2: Upload the runbook to the Azure SRE Agent Knowledge base
- Task 3: Verify indexing and knowledge inventory
- Task 4: Compare generic and runbook-grounded incident responses
- Task 5: Refine the knowledge-grounded response

## Task 1: Review the local App Service HTTP 500 runbook
In this task, you will open the prepared Markdown runbook on the Lab VM and identify the operational details the agent should use later.

1. If your SRE Agent portal session has expired, open <https://sre.azure.com> and sign in with the lab credentials:

   - Username: <inject key="AzureAdUserEmail"></inject>
   - Password: <inject key="AzureAdUserPassword"></inject>

2. On the Lab VM, open **File Explorer**.

3. Browse to **C:\LabFiles\Runbooks**.

4. Open **appservice-http-500-triage.md** in Notepad, Visual Studio Code, or another text editor.

5. Review the runbook and note the sections that are specific to this lab scenario. Look for guidance such as:

   - HTTP 500 symptoms for the sample App Service workload.
   - First checks in Azure App Service diagnostics.
   - Application Insights and Log Analytics investigation steps.
   - KQL query examples for failed requests, exceptions, and dependencies.
   - Escalation criteria and mitigation guidance.

6. Keep the file location open. You will upload this exact file in the next task.

> [!Note]
> Azure SRE Agent supports persistent knowledge uploads for runbooks and troubleshooting guides. The prepared runbook is a Markdown file, which is a supported format for Knowledge base uploads.

## Task 2: Upload the runbook to the Azure SRE Agent Knowledge base
In this task, you will add the runbook as long-term knowledge for the agent. Files uploaded to the Knowledge base are indexed so the agent can search and reference them in future conversations.

1. In your browser, go to <https://sre.azure.com>.

2. Select the Azure SRE Agent that you created or verified in Exercise 1.

3. Confirm that you are working in the lab subscription <inject key="SubscriptionID"></inject> and tenant <inject key="TenantID"></inject>.

4. In the left navigation, select **Builder**.

5. Select **Knowledge base**.

   > [!Tip]
   > Some portal builds may label the same area as **Knowledge sources** or **Knowledge settings**. Use the page under **Builder** that lets you add files, view source names, and see indexing status.

6. Select **Add file**.

7. In the file picker, browse to **C:\LabFiles\Runbooks**.

8. Select **appservice-http-500-triage.md**.

9. Select **Open**, and then select **Add file** or **Upload** if the portal asks for confirmation.

10. Verify that **appservice-http-500-triage.md** appears in the knowledge source list.

> [!Important]
> For this exercise, upload the runbook through the Knowledge base rather than attaching it to a single chat message. A chat attachment is useful for one conversation, but a Knowledge base upload persists at the agent level and is searchable in future chats.

## Task 3: Verify indexing and knowledge inventory
In this task, you will wait for the file to become searchable and then ask the agent what operational procedures it has available.

1. On the **Knowledge base** page, locate **appservice-http-500-triage.md**.

2. Wait until the file status shows **Indexed** or a comparable ready state.

   > [!Note]
   > Microsoft Learn describes indexing as usually quick. If the status remains **Pending**, wait 1 to 2 minutes and refresh the page. If the status changes to **Not indexed**, upload the file again and confirm that you selected the Markdown file from **C:\LabFiles\Runbooks**.

3. Start a new chat with the agent, or return to the main chat area.

4. Ask the agent the following knowledge inventory prompt:

   ```text
   What runbooks or procedures do you have in your knowledge base?
   ```

5. Review the response and confirm that it references **appservice-http-500-triage.md** or describes an App Service HTTP 500 triage procedure.

6. If the answer does not mention the uploaded runbook, ask a more specific follow-up:

   ```text
   Search your knowledge base for the App Service HTTP 500 triage runbook. What procedure did you find?
   ```

7. Confirm that the response includes at least one runbook-specific detail, such as **HTTP 500**, **Application Insights**, **KQL**, **App Service diagnostics**, or **escalation**.

> [!Tip]
> Good evidence includes a visible **Sources** section or citation link showing the uploaded runbook file name. If sources are available, open the citation to confirm it points to the runbook content.

## Task 4: Compare generic and runbook-grounded incident responses
In this task, you will compare a general troubleshooting answer with a runbook-grounded incident response. This helps you verify that uploaded operational knowledge changes the quality and specificity of the agent's answer.

1. In the agent chat, ask a broad troubleshooting question first:

   ```text
   What are common causes of HTTP 500 errors in Azure App Service?
   ```

2. Read the response. It may include general causes such as application exceptions, dependency failures, configuration issues, deployment regressions, or platform health checks.

3. Now ask the runbook-grounded incident triage prompt:

   ```text
   The web app is returning intermittent HTTP 500 errors. Use the uploaded runbook and the Azure resources you can access to recommend first checks and escalation criteria.
   ```

4. Compare the second response with the broad answer. The runbook-grounded response should be more specific to this lab and should include guidance similar to the prepared runbook, such as:

   - Checking the lab App Service and its diagnostics blade.
   - Reviewing Application Insights failed requests, exceptions, dependencies, and traces.
   - Using KQL examples or KQL-style investigation steps.
   - Looking for dependency failures, recent changes, or repeated exception patterns.
   - Applying escalation criteria rather than treating every HTTP 500 as the same severity.

5. If the response is still too generic, ask the agent to explicitly cite the uploaded runbook:

   ```text
   Answer again, but cite the uploaded App Service HTTP 500 triage runbook and separate runbook guidance from general Azure guidance.
   ```

6. Review the grounded response and identify which parts came from the runbook versus general Azure troubleshooting knowledge. You will use this response as the starting point for the checklist refinement in the next task.

> [!Note]
> The lab workload resources are deployed in the resource group for deployment <inject key="DeploymentID" enableCopy="false"></inject>. If the agent cannot discuss the workload resources, return to Exercise 1 and confirm that the agent has access to the workload resource group before continuing.

## Task 5: Refine the knowledge-grounded response
In this task, you will turn the runbook-grounded triage answer into an actionable incident checklist for the App Service HTTP 500 scenario. The goal is to practice steering the agent from a helpful explanation toward a response format that an on-call SRE could follow during an active incident.

1. In the same chat thread, ask the agent to convert the runbook-grounded response into a checklist:

   ```text
   Turn your runbook-grounded HTTP 500 triage answer into an actionable checklist for the on-call SRE. Keep it specific to the lab App Service incident and include what to check, where to check it, and what signal would trigger escalation.
   ```

2. Review the checklist for operational structure. A useful checklist should be ordered, concise, and action oriented. Confirm that it includes items such as:

   - Confirm the impacted Azure App Service and current HTTP 500 symptom pattern.
   - Check App Service diagnostics or platform health signals.
   - Review Application Insights failed requests, exceptions, dependencies, or traces.
   - Use KQL or KQL-style queries to isolate time windows, exception types, or dependency failures.
   - Apply the runbook's escalation criteria when the signal indicates repeated failures, customer impact, or unresolved dependency issues.

3. Confirm that the checklist references the uploaded **appservice-http-500-triage.md** runbook or shows **Sources** for that file. If the answer does not clearly use the runbook, ask this follow-up:

   ```text
   Revise the checklist so it explicitly cites the uploaded App Service HTTP 500 triage runbook and marks which checklist items came from that runbook.
   ```

4. Confirm that the refined checklist includes at least two Azure operational signals from the scenario. Acceptable signals include:

   - **Application Insights** failed requests, exceptions, dependencies, traces, or transaction search.
   - **KQL** queries or query logic for failed requests, exceptions, or dependency failures.
   - **App Service diagnostics** checks for the web app.
   - Dependency failure patterns or downstream service errors.
   - Escalation criteria from the uploaded runbook.

5. If the checklist is missing clear decision points, ask the agent to add them:

   ```text
   Add decision points to the checklist. For each step, include the signal to look for and the next action if that signal is present.
   ```

6. Optionally, ask the agent to critique the runbook for gaps that would make the next HTTP 500 incident easier to handle:

   ```text
   Based on the checklist you created, what details are missing from the uploaded runbook that our team should add before the next incident?
   ```

7. Review the suggested improvements. Useful suggestions might include adding owner contacts, dependency names, exact KQL queries, severity definitions, rollback criteria, or links to dashboards.

> [!Tip]
> Strong incident checklists combine team-specific runbook guidance with live Azure signals. If the response only gives generic advice, continue prompting the agent to use **appservice-http-500-triage.md** and to name the Azure signal that supports each action.

## 🧾 Summary
You uploaded the App Service HTTP 500 triage runbook to Azure SRE Agent, waited for indexing, and verified that the agent could discover and use the runbook in chat. You also compared generic troubleshooting guidance with a runbook-grounded incident response and refined that response into an actionable checklist for the lab's intermittent HTTP 500 incident scenario. The agent is now configured to use team operational knowledge when responding to the lab workload.

🎉 You have successfully finished the lab. In this lab, you onboarded Azure SRE Agent against a sample Azure incident environment, scoped it to least-privilege Reader access over the workload resource group, and grounded its incident-triage responses in your team's own HTTP 500 runbook — turning a generic troubleshooting assistant into one that reflects your organization's documented operational practice.
