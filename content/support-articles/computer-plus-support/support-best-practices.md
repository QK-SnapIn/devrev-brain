---
title: Support best practices
devrev_id: ART-21863
parent_directory: Computer+ Support
translation_group: K_Q8Upm_
modified_date: "2026-04-09T10:48:49.997Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/K_Q8Upm_"
tags: []
top_category: Computer+ Support
wiki_match: support-app
match_score: 0.545
last_updated: 2026-05-11
summary: "+ Pain points and primary use cases + Success plan for the account + Meeting notes and meeting recordings + Next steps and action items Define a small number of tags to help categorize tickets."
---

# Support best practices

## Configure the DevRev app

* Install and configure the support convergence, auto-response, and [[entities/article|article]] suggestion [snap-ins](https://devrev.ai/marketplace) so that customer [[features/conversations-feature|conversations]] are acknowledged automatically.
* Ensure that every customer org record in DevRev contains the following:

  + Pain points and primary use cases
  + Success plan for the [[entities/account|account]]
  + [[entities/meeting|Meeting]] notes and meeting recordings
  + Next steps and action items
* Define a small number of tags to help categorize [[features/tickets|tickets]]. For example, at DevRev we have the following: `bug`, `feature-request`, `other-request`, `question`, and `incident`.
* Designate one or more customer experience engineers to be on call. Add them to the **Support** [[entities/group|group]] inside [**Settings > Groups**](https://app.devrev.ai/?setting=groups) and as default owner in the **Support Routing** snap-in. Default owners are notified through email and the DevRev app as soon as a new [[entities/conversation|conversation]] is started.

## Monitor the inbox

* Periodically group the **[[features/inbox|Inbox]]** by stage and make sure there conversations only in *hold* or *awaiting customer response* stages.
* Let the customer know when a [[entities/ticket|ticket]] linked to a conversation is closed and request their verification.
* Once all tickets of a conversation are resolved and the customer is satisfied, resolve the conversation.
* Move new tickets to the *awaiting product assist* stage.

## Respond to conversations

* Respond as fast as possible to any new conversation. Respond within 1 hour to new messages on existing conversations. Change the stage of conversation to *awaiting customer response* as soon as you have responded.
* In **Updates**, filter by **Type** > **Mentioned**. Respond to those updates first.
* Create a ticket if you aren't able to resolve the conversation in 20 minutes. As soon as the ticket is opened, move it to the *escalate* stage. The owner of the ticket is the owner of the customer org where the conversation originated, usually someone from customer success or sales.
* Ask follow-up questions to get the full context of the problem.
* If the article suggestion didn't help the user, [[features/search|search]] in the customer-facing documentation or [[features/knowledge-base|knowledge base]] and share any relevant results.
* If you receive any spam messages, you can choose the **Mark as Spam** option, which will prompt a pop-up. To mark the sender as spam, select the **Mark all as spam** option in the pop-up.
* If you are tagged on a conversation of which you are not the owner, let the owner know to respond. It's beneficial to retain the same point of contact for the duration of the conversation unless the owner refers some another user.
* If the conversation has a customer org that's unidentified or is new, add yourself (the customer experience engineer) as the owner of the ticket. Try to find the appropriate owner for the customer org and update the customer record accordingly.
* Change the stage of the conversation to hold if there are tickets linked. This means that support is asking for help from engineering.

## Internal discussions

Use the **Internal discussions** tab to coordinate with team members directly within a conversation thread. The **Internal discussions** tab is visible only to internal users. Customers aren’t notified.

Start an internal discussion when you need to:

* **Clarify customer [[features/issues|issues]]**: Consult with team members or subject matter experts when you need more context to resolve a complex [[entities/issue|issue]].
* **Qualify potential sales leads**: For messages that may indicate a sales [[glossary/opportunity|opportunity]], such as pricing or demo requests, discuss with Sales or Customer Success before responding.
* **Route or escalate conversations**: If you’re unsure who should own a conversation, align internally before reassigning or escalating it. Use the discussion to document ownership or stage changes.
* **Maintain response consistency**: When multiple team members collaborate on a reply, use internal discussions to agree on messaging before responding to the customer.

## Conduct daily health checks

* On a daily basis all ticket owners should triage tickets to make sure they're well-maintained and that appropriate actions are taken.
* Move new tickets from *queued* to the *awaiting product assist*.
* Track the default **Team Activity** [[glossary/vista|vista]] for tickets owned by everyone and navigate to your tickets. Ensure the correct owners are assigned; tickets should be assigned only to revenue team members.

## Manage tickets

* Regularly follow up with the customer on any ticket in the *awaiting customer* stage. If no response is forthcoming in a reasonable amount of time as defined by your [[features/slas|SLA]], mark the ticket as *resolved*.
* Critically assess the severity of the ticket according to the impact on the customer’s business. Blockers are those tickets that are critical to customer adoption or operations. Each account should have some balance of high, medium, and low severity issues.
* If the customer states any new concerns or requests in the course of discussions on a ticket, open new tickets and create associations.
* If the customer does not confirm the resolution, move the ticket back to *in development* and let the engineering/PM team know of the feedback.
* Provide regular updates to customers on open/in-progress tickets. The proper update frequency is determined by the severity of the ticket.
* Make sure all tickets have the customer org field populated.
* Cancel any internal ticket without a customer org that has been created by a developer. Ask them to create an issue instead.
* If a customer raises a feature request that aligns with the product strategy, but needs significant development effort and will not be delivered in the near future, move it to the *accepted* stage, rather than keeping the ticket open. Inform the customer accordingly.
* If a customer reports a concern that the documentation on the public site is incorrect, missing, or insufficient, open a ticket so that the [[entities/part|part]] owner can update the documentation or route the report to someone who can.

## Source
- DevRev support article [Support best practices](https://support.devrev.ai/en-US/devrev/article/K_Q8Upm_) (ART-21863)
