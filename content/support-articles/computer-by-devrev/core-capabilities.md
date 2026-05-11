---
title: Core capabilities
devrev_id: ART-24048
parent_directory: Computer by DevRev
translation_group: 7sw49sh0
modified_date: "2026-05-01T02:16:27.113Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/7sw49sh0"
tags: []
top_category: Computer by DevRev
wiki_match: features/conversations
match_score: 0.467
last_updated: 2026-05-11
summary: "Computer is designed to be your primary AI teammate, capable of searching, synthesizing, and creating content based on your organization\"s data."
---

# Core capabilities

Computer is designed to be your primary AI teammate, capable of searching, synthesizing, and creating content based on your organization's data.

# Find information

Computer provides a unified [[features/search|search]] across all your connected work applications. You no longer need to switch between multiple tabs or tools.

## How it works

Performs keyword and semantic searches across your connected applications, such as Slack, Jira, and Notion, as well as DevRev objects like [[features/tickets|tickets]] and [[features/accounts|accounts]].

Example prompts:

* Find the latest PRD for the mobile app project.
* Which tickets are related to the installation package problem?
* Who is the primary contact for the Acme [[entities/account|account]]?

# Answers and summarization

Computer goes beyond simply finding data. It synthesizes complex information from multiple sources and delivers clear, concise answers..

## How it works

Analyzes long comment threads, documentation, and external web sources to generate direct answers and summaries.

## Information sources

* Connected apps: Notion, Google Drive, SharePoint, Slack, and Microsoft Teams.
* DevRev system of record (SoR): Tickets, [[features/issues|issues]], [[entities/opportunity|opportunities]], and accounts.
* Web search: Real-time information from the internet, such as industry trends or competitor news.

Example prompts

* Summarize the last 10 comments on [[entities/ticket|ticket]] TKT-1410.
* What are the common themes across our recent support escalations?
* Give me an account summary for the Neo [[entities/group|Group]].

# Co-creation

Computer serves as a collaborative drafting partner for your work-related communications and documentation.

## How it works

It helps you draft emails, write formatted PRDs, brainstorm project ideas, and edit existing text to change tone or clarity.

Example prompts

* Draft a follow-up email to the customer regarding their feature request.
* Help me write a formatted PRD based on these notes.
* Brainstorm five potential names for our new internal AI bot.

# File Upload

You can bring external data directly into a [[entities/conversation|conversation]] for immediate analysis.

* Supported file types: PDF, TXT, and CSV.
* How to upload: Drag and drop files directly into the chat interface or use the attachment icon in the message bar.
* What Computer can do with files:

  + Analyze and summarize: Extract key takeaways from long reports or RFP documents.
  + Reference: Use the uploaded file as the primary context for follow-up questions, such as filling out a questionnaire based on an attached PRD.
* File size limits: You can upload PDF files up to 25 MB and TXT files up to 2 MB.
* Privacy and retention: Uploaded files are processed within your organization's secure environment and follow standard DevRev data residency and compliance policies.

# Web search

Computer can search the live web in real-time to find current information beyond your organization's internal data sources.

## How it works

Computer performs real-time searches across the internet to retrieve up-to-date information, news, industry trends, competitor intelligence, and general knowledge that may not exist in your connected apps or DevRev objects.

### When Computer uses web search vs connected apps

Computer intelligently selects the most relevant data source to use based on your query.

Web Search is used for:

* Current events, news, and real-time information such as stock prices, weather, recent announcements
* Industry trends and market research
* Competitor analysis and public company information
* General knowledge questions and definitions
* Technical documentation for public tools and frameworks
* Information about people, companies, or topics not in your internal systems

Connected Apps are prioritized for:

* Internal documents, PRDs, and company-specific content
* Team communications and Slack or Teams discussions
* Project management data from tools such as Jira
* Customer account information and support tickets
* Proprietary business data and internal knowledge bases

Computer can combine information from both web search and connected apps when necessary. For example, Computer may use multiple sources when researching a prospect or conducting competitive analysis.

Example prompts

* Find recent news about generative AI regulations in the EU
* Search the web and give me a summary of the news coverage around Computer’s launch

# Conversational Analytics (text to SQL)

Conversational [[features/analytics|Analytics]] transforms your natural language questions into SQL queries behind the scenes, allowing you to instantly analyze your data without writing code or building custom reports. Computer intelligently queries your organization's data including tickets, opportunities, accounts, issues, and even custom objects and fields, to provide accurate analytical insights.

## How it works

* **Multi-object queries**: Analyze data that spans multiple object types, such as opportunities linked to tickets or issues connected to [[entities/enhancement|enhancements]]
* **Graph traversal**: Navigate complex relationships between objects, including parent-child hierarchies, linked entities, and dependencies
* **Aggregations and analytics**: Get counts, distributions, breakdowns, and summaries across your data with grouping and filtering
* **Custom object support**: Query your organization's custom objects and custom fields with the same ease as standard DevRev objects

Example prompts

* How many tickets are currently open?
* Break all the tickets down by severity.

# Actions

Computer can perform actions on your behalf, such as creating tickets, making issues, or conducting web searches.

## Human-in-the-loop approval flow

Enable the **Needs Approval** setting when configuring actions under **Settings**. When enabled, Computer will always ask for your confirmation before executing any action.

Example prompts

* Please create an [[entities/issue|issue]] for me to track the launch for login features
* Please update the owner of TKT-123 to John

# Customize Computer

You can add actions that integrate with DevRev by going to the Customize Computer tab under Settings.

**Note**: Only admins can add actions in Computer.

![img10.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/9179124&key=3d729686b2689152acbaeebbd98c489d7307340a42fb09217a2beec6e7582968)

## Source
- DevRev support [[entities/article|article]] [Core capabilities](https://support.devrev.ai/en-US/devrev/article/7sw49sh0) (ART-24048)
