---
title: Workflow action library
devrev_id: ART-21901
parent_directory: Workflow engine
translation_group: I5gcoCnY
modified_date: "2026-01-29T11:17:40.177Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/I5gcoCnY"
tags: []
top_category: Computer by DevRev
wiki_match: features/workflows
match_score: 0.615
last_updated: 2026-05-11
summary: "When a workflow starts running, the action steps define which operations or processes occur and specify any data that needs to be transferred between blocks."
---

# Workflow action library

When a workflow starts running, the action steps define which operations or
processes occur and specify any data that needs to be transferred between
blocks. Below is a list the action steps you can use.

## Object creation

| Operation | Description | Input Parameters | Output |
| --- | --- | --- | --- |
| Create [[entities/account|Account]] | Creates a new account in DevRev. | * Account details like name, description, domains, etc. * subtype: (Optional) Account subtype * apps: (Optional) Related apps * app\_custom\_fields: (Optional) Custom fields | Created account object |
| Create Contact | Creates a new contact (rev\_user) in DevRev. | * Contact details like email, full\_name, phone, etc. * subtype: (Optional) Contact subtype * apps: (Optional) Related apps * app\_custom\_fields: (Optional) Custom fields | Created rev\_user object |
| Create [[glossary/incident|Incident]] | Creates a new incident in DevRev. | * Incident details like title, body, applies\_to\_part, etc. * subtype: (Optional) Incident subtype * apps: (Optional) Related apps * app\_custom\_fields: (Optional) Custom fields | Created incident object |
| Create [[entities/issue|Issue]] | Creates a new issue in DevRev. | * Issue details like title, body, priority\_v2, etc. * subtype: (Optional) Issue subtype * apps: (Optional) Related apps * app\_custom\_fields: (Optional) Custom fields | Created issue object |
| Create [[entities/meeting|Meeting]] | Creates a new meeting in DevRev. | * Meeting details like title, description, start\_date, attendees, etc. * subtype: (Optional) Meeting subtype * apps: (Optional) Related apps * app\_custom\_fields: (Optional) Custom fields | Created meeting object |
| Create [[glossary/opportunity|Opportunity]] | Creates a new opportunity in DevRev. | * Opportunity details like title, body, applies\_to\_part, etc. * subtype: (Optional) Opportunity subtype * apps: (Optional) Related apps * app\_custom\_fields: (Optional) Custom fields | Created opportunity object |
| Create [[entities/ticket|Ticket]] | Creates a new ticket in DevRev. | * Ticket details like title, body, applies\_to\_part, etc. * subtype: (Optional) Ticket subtype * apps: (Optional) Related apps * app\_custom\_fields: (Optional) Custom fields | Created ticket object |
| Convert [[entities/conversation|Conversation]] To Ticket | Converts a conversation to a ticket. | * conversation\_id: ID of the conversation to convert | ticket\_id: ID of the created ticket |

## Object retrieval

| Operation | Description | Input Parameters | Output |
| --- | --- | --- | --- |
| GetAccount | Retrieves account details. | * id: ID of the account * subtype: (Optional) Account subtype * apps: (Optional) Related apps | Account object |
| GetAirdropSyncUnit | Retrieves information about an [[glossary/airdrop|Airdrop]] sync unit. | * id: ID of the sync unit | Sync unit object |
| GetConversation | Retrieves conversation details. | * id: ID of the conversation * subtype: (Optional) Conversation subtype * apps: (Optional) Related apps | Conversation object |
| GetCustomer | Retrieves customer (rev\_user) details. | * id: ID of the customer * subtype: (Optional) Customer subtype * apps: (Optional) Related apps | Rev\_user object |
| GetEnhancement | Retrieves [[entities/enhancement|enhancement]] details. | * id: ID of the enhancement * subtype: (Optional) Enhancement subtype * apps: (Optional) Related apps | Enhancement object |
| GetFeature | Retrieves feature details. | * id: ID of the feature * subtype: (Optional) Feature subtype * apps: (Optional) Related apps | Feature object |
| GetIncident | Retrieves incident details. | * id: ID of the incident | Incident object |
| GetIssue | Retrieves issue details. | * id: ID of the issue * subtype: (Optional) Issue subtype * apps: (Optional) Related apps | Issue object |
| GetMeeting | Retrieves meeting details. | * id: ID of the meeting * subtype: (Optional) Meeting subtype * apps: (Optional) Related apps | Meeting object |
| GetOpportunity | Retrieves opportunity details. | * id: ID of the opportunity * subtype: (Optional) Opportunity subtype * apps: (Optional) Related apps | Opportunity object |
| GetOrgUser | Retrieves organization user details. | * id: ID of the user * subtype: (Optional) User subtype * apps: (Optional) Related apps | Dev\_user object |
| GetOrgUserPreference | Retrieves user preferences. | * id: ID of the user | User preference object |

## Object updates

| Operation | Description | Input Parameters | Output |
| --- | --- | --- | --- |
| UpdateAccount | Updates account details. | * id: ID of the account to update * Account details to update * subtype: (Optional) Account subtype * apps: (Optional) Related apps * app\_custom\_fields: (Optional) Custom fields | Updated account object |
| UpdateContact | Updates contact (rev\_user) details. | * id: ID of the contact to update * Contact details to update * subtype: (Optional) Contact subtype * apps: (Optional) Related apps * app\_custom\_fields: (Optional) Custom fields | Updated rev\_user object |
| UpdateConversation | Updates conversation details. | * id: ID of the conversation to update * Conversation details to update * stage\_name: (Optional) New stage | Updated conversation object |
| UpdateEnhancement | Updates enhancement details. | * id: ID of the enhancement to update * Enhancement details to update * subtype: (Optional) Enhancement subtype * apps: (Optional) Related apps * app\_custom\_fields: (Optional) Custom fields | Updated enhancement object |
| UpdateIncident | Updates incident details. | * id: ID of the incident to update * Incident details to update * subtype: (Optional) Incident subtype * apps: (Optional) Related apps * app\_custom\_fields: (Optional) Custom fields * stage: (Optional) New stage | Updated incident object |
| UpdateIssue | Updates issue details. | * id: ID of the issue to update * Issue details to update * subtype: (Optional) Issue subtype * apps: (Optional) Related apps * app\_custom\_fields: (Optional) Custom fields * stage: (Optional) New stage | Updated issue object |
| UpdateMeeting | Updates meeting details. | * id: ID of the meeting to update * Meeting details to update * subtype: (Optional) Meeting subtype * apps: (Optional) Related apps * app\_custom\_fields: (Optional) Custom fields | Updated meeting object |
| UpdateOpportunity | Updates opportunity details. | * id: ID of the opportunity to update * Opportunity details to update * subtype: (Optional) Opportunity subtype * apps: (Optional) Related apps * app\_custom\_fields: (Optional) Custom fields * stage: (Optional) New stage | Updated opportunity object |
| UpdateQuestionAnswer | Updates a question and answer pair. | * id: ID of the Q&A to update * question: (Optional) Updated question * answer: (Optional) Updated answer * Other Q&A properties | Updated question\_answer object |
| UpdateTicket | Updates ticket details. | * id: ID of the ticket to update * Ticket details to update * subtype: (Optional) Ticket subtype * apps: (Optional) Related apps * app\_custom\_fields: (Optional) Custom fields * stage: (Optional) New stage | Updated ticket object |

## Object links

| Operation | Description | Input Parameters | Output |
| --- | --- | --- | --- |
| LinkConversationWithTicket | Creates a link between a conversation and a ticket. | * source: Conversation ID * link\_type: Type of link (usually "is\_related\_to") * target: Ticket ID | Empty response on success |
| LinkIncidentWithIssue | Creates a link between an incident and an issue. | * source: Incident ID * link\_type: Type of link (usually "is\_dependent\_on") * target: Issue ID | Empty response on success |
| LinkIssueWithIssue | Creates a link between two [[features/issues|issues]]. | * source: Source issue ID * link\_type: Type of link * target: Target issue ID | Empty response on success |
| LinkTicketWithIssue | Creates a link between a ticket and an issue. | * source: Ticket ID * link\_type: Type of link (usually "is\_dependent\_on") * target: Issue ID | Empty response on success |
| ListObjectsLinkedToIssue | Retrieves objects linked to an issue. | * issue: ID of the issue * objects: Types of objects to find * relationship: (Optional) Specific relationship types to filter by | Array of linked objects with relationship information |
| ListObjectsLinkedToTicket | Retrieves objects linked to a ticket. | * ticket: ID of the ticket * objects: Types of objects to find * relationship: (Optional) Specific relationship types to filter by | Array of linked objects with relationship information |

## Communication and notification

| Operation | Description | Input Parameters | Output |
| --- | --- | --- | --- |
| AddComment | Adds a comment to an object in DevRev. Supports various visibility options and user permissions. | * object: ID of the object * body: Comment body * visibility: (Optional) "external", "internal", or "private" * users: (Required if visibility is "private") List of users who can   see the comment | * id: ID of the created comment * created\_by: User who created the comment |
| AskOptions | Displays a message with interactive buttons that users can click. | * object: ID of the object * message: (Optional) Message text * buttons: Array of buttons with name and display\_name * visibility: (Optional) Visibility setting * panel: (Optional) Panel to display the message * private\_to: (Optional) Users for private visibility | Output ports created dynamically based on button clicks |
| SendNotification | Sends a notification to specified users or [[entities/group|groups]]. | * receivers: Users or groups who will receive the notification * body: The body of the notification * title: The title of the notification * linked\_object: (Optional) The object which will open on clicking the   notification | Empty response on success |

## Source
- DevRev support [[entities/article|article]] [Workflow action library](https://support.devrev.ai/en-US/devrev/article/I5gcoCnY) (ART-21901)
