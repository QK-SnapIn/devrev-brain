---
title: Questions & Answers
devrev_id: ART-21865
parent_directory: Knowledge Base
translation_group: CJlxZ9G3
modified_date: "2026-03-26T18:25:51.243Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/CJlxZ9G3"
tags: []
top_category: Computer+ Support
wiki_match: features/conversations
match_score: 0.467
last_updated: 2026-05-11
---

# Questions & Answers

Questions & Answers (Q&As) refer to a collection of commonly posed questions and their answers regarding a particular product, service, or topic. The Q&A feature on DevRev works as an additional knowledge source for [[support-articles/computer-plus-support/computer-for-your-customers|Computer for Your Customers]] to answer customer queries in conversations to provide efficient customer support.

Unlike knowledge [[support-articles/computer-plus-support/articles|articles]], Q&As are never quoted as sources to the end user.

Q&As can be created either manually or automatically from your customer conversations by Computer.

## Manual creation

In the following cases, you may choose to create Q&As manually:

* Website FAQs that you prefer not to display as articles but are crucial for Computer to effectively respond to customer inquiries.
* Internal documentation that's not intended for public search but is valuable for enhancing response quality.
* Details about bugs or issues in Q&As that shouldn't be publicly searchable in your knowledge base and are not relevant to all customers but are essential for Computer to address specific customer questions.

To create a Q&A, do the following:

1. Go to [**Settings** > **Turing** > **Q&As**](https://app.devrev.ai/?setting=question-answers) and click **+ QA** in the top-right corner.
2. Fill in the **Question** and **Answer** fields, and select the relevant **Part**.
3. Set the appropriate **Status** and **Access level**. Set the status to *External* or *Public* if you want Computer to use it.
4. Confirm by clicking **Create**.

![Computer status](don:core:dvrv-us-1:devo/0:artifact/4100065)

## Automatic creation

Your customer conversations include a lot of knowledge, including some of the most accurate and current information. With the automated creation of Q&As, Computer learns from customer conversations in which a human answers a question that it previously could not answer.

When a customer initiates a conversation seeking answers, Computer springs into action, drawing upon published Q&As and knowledge articles to provide a solution. If Computer falls short or the user prefers a more personalized touch, they opt to connect with a customer experience engineer and resolve the conversation. Computer doesn't just move on—it learns. It autonomously generates new Q&As based on the resolved conversation, marking them for review under the *Review Needed* status.

A Q&A isn't created if it is similar to the existing Q&A to avoid duplication.

![Q&A Process Diagram](don:core:dvrv-us-1:devo/0:artifact/4100068)

To enable automatic creation, under [**Settings** > **Turing** > **Q&As**](https://app.devrev.ai/?setting=question-answers), go to **Preferences** on the top right and enable **Auto generate Q&As** and click **Save**.

You need to be an admin to set preferences.

![conversation Q&A](don:core:dvrv-us-1:devo/0:artifact/4100074)

When Computer creates a new Q&A, the conversation's owner receives a notification. It's their chance to ensure accuracy before deciding whether to *Publish* them if needed or *Archive* if not.

Once approved and published, these Q&As enter Computer's knowledge base, ready to tackle similar questions in the future. Each conversation can generate unique Q&As, increasing Computer's knowledge base with every interaction.

Every Q&A is intricately linked to its originating conversation, preserving the context of its creation. Even if initially overlooked, support team members can revisit pending Q&As by filtering [**Settings** > **Turing** > **Q&As**](https://app.devrev.ai/?setting=question-answers) for those in the *Review Needed* state.

![review](don:core:dvrv-us-1:devo/0:artifact/4100078)

## Searching for Q&As

Search for a previously created Q&A on the DevRev app by pressing `cmd+K` on Mac or `Ctrl+K` on Windows. Q&As appear within the KB section of the Search bar. You can search Q&As by entering keywords within a Question or Answer.

## Q&A structure

* **Question**: Define the customer query.
* **Answer**: Provide the corresponding solution or information.
* **Part**: Choose the product or service area the Q&A pertains to.
* **Status**: Determine the progress phase of the Q&A.

  + *Published*: These Q&As are live and actively used by Computer to answer customer queries in conversations.
  + *Draft*: Indicates that the Q&A is still being written or is a work in progress.
  + *Review needed*: If the author requires validation, the QA can be marked for review, typically by a manager or designated reviewer.
  + *Archived*: Denotes Q&As that have become redundant, incorrect, or obsolete.
* **Access Level**: Determine who can view and access the Q&A.

  + *Private / Internal / Restricted*: Not visible to external users, not used by the agent, and only searchable within the app.
  + *External / Public*: Available for all, Computer employs these Q&As extensively, and they appear in search results both for app users and portal and Plug visitors.

## Source
- DevRev support article [Questions & Answers](https://support.devrev.ai/en-US/devrev/article/CJlxZ9G3) (ART-21865)
