---
title: ClickUp AirSync
devrev_id: ART-22016
parent_directory: AirSync
translation_group: lJJ1JBVg
modified_date: "2026-01-05T05:42:02.21Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/lJJ1JBVg"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "Experience hassle-free import of your ClickUp tasks into DevRev with DevRev\"s ClickUp AirSync."
---

# ClickUp AirSync

Experience hassle-free import of your ClickUp [[entities/task|tasks]] into DevRev with DevRev's ClickUp [[glossary/airsync|AirSync]].

## Supported objects

The following is a list of ClickUp objects and their corresponding DevRev
equivalent. Those marked as **Supported** are eligible for import.

| ClickUp object | DevRev object | Sync to DevRev |
| --- | --- | --- |
| [[entities/task|Task]] | [[entities/issue|Issue]] (or [[entities/ticket|ticket]]) | ✅ |
| Tag | Tags | ✅ |
| Comment | Timeline comments | ✅ |
| User | DevUser | ✅ |
| User [[entities/group|group]] | Group | ❌ |
| Attachment | Attachment | ❌ |

**Spaces**, **Folders**, and **Lists** are imported as custom fields within the issue/ticket object. The objects to import can be filtered based on their values if you select it so in the **Mappings required** phase.

ClickUp tasks are imported as [[features/issues|issues]] by default. You can choose to have them imported as [[features/tickets|tickets]] if required.For the sake of preserving existing structure, DevRev work items (issues or tickets) are created with the same hierarchical structure as the source tasks in ClickUp. That is, ClickUp tasks with child tasks become DevRev issues with child issues or tickets with child tickets.However, while the DevRev UI allows you to create parent/child relationships between issues, you cannot do the same with tickets. If your workflow requires manual creation of parent/child relationships in DevRev work items, you should use issues. If that is not a requirement and tickets are preferred for another reason, you can specify tickets as the target for ClickUp tasks.

## Import from ClickUp

Follow the steps below to import from ClickUp:

1. In **Marketplace**, [[features/search|search]] for **ClickUp** and install the snap-in.
2. In the snap-in config modal, click **Install** then go to **Integrations** > **AirSyncs** in your settings left nav.
3. Click the **AirSync** import button and select the **ClickUp** tile in the **Start import** window.
4. Create a new connection to your ClickUp [[entities/account|account]], or use an existing connection if you already have one.While creating the connection, you are required to input a **Subdomain** field. This is a mandatory unique identifier to group together AirSyncs from the same source system, and does not affect the import process.It is recommended to use the ID of the ClickUp workspace you want to import as the value of **Subdomain**.
5. Once the connection is established, select the ClickUp workspace you want to import and specify the DevRev [[entities/part|part]] that should be used for any imported work. This initiates a bulk import of the selected site.
6. Click **Map fields** in the import row and configure filters, object mapping, or field mapping as necessary.If you want ClickUp tasks to become tickets rather than issues, map the `task` object to `Works.Issue`.While DevRev attempts to automatically map fields, you may be prompted to manually map indicated fields.

The duration of the import depends on the size of the ClickUp workspace and the
data being imported. It can take seconds for a workspace with only a few dozen
tasks to a few hours for a workspace with tens of thousands of
items with many attachments. DevRev honors the ClickUp API rate limits and
back-off and resumes automatically.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support [[entities/article|article]] [ClickUp AirSync](https://support.devrev.ai/en-US/devrev/article/lJJ1JBVg) (ART-22016)
