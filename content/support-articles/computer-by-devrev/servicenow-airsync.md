---
title: ServiceNow AirSync
devrev_id: ART-22008
parent_directory: AirSync
translation_group: GujEKqBQ
modified_date: "2026-01-28T21:42:11.043Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/GujEKqBQ"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/airsync
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/airsync']
summary: "DevRev\"s ServiceNow import allows you to perform a sync from ServiceNow to DevRev."
---

# ServiceNow AirSync

DevRev's ServiceNow import allows you to perform a sync from ServiceNow to DevRev. The ServiceNow [[glossary/airsync|AirSync]] focuses on [ITSM](https://www.servicenow.com/products/itsm.html) and [CSM](https://www.servicenow.com/products/customer-service-management.html) products of ServiceNow.

## Supported objects

The following is a list of ServiceNow objects and their corresponding DevRev
equivalent.

|  |  |  |  |
| --- | --- | --- | --- |
| ServiceNow Object | DevRev Object | Sync to DevRev | Sync to ServiceNow |
| [[entities/task|Task]] (\* all subtype of task) | [[entities/ticket|Ticket]] | ✅ | ✅ |
| [[glossary/incident|Incident]] | Incident | ✅ | ✅ |
| Incident Task | Incident | ✅ | ✅ |
| Comments | Comment on Ticket | ✅ | ✅ |
| Attachments | Attachment on Ticket | ✅ | ✅ |
| [[entities/account|Account]] | Account | ✅ | ❌ |
| Contact | RevUser | ✅ | ❌ |
| Consumer | RevUser | ✅ | ❌ |
| RevUser | RevUser | ✅ | ❌ |
| Agent | DevUser | ✅ | ❌ |

All subtypes of task are imported as [[features/tickets|tickets]]. The task table in ServiceNow can be extended to create custom table types.

Below is a list of common task subtypes that are supported for import. The format shown is **ServiceNow Label / DevRev Subtype Name (servicenow\_table\_name)**,

where the first [[entities/part|part]] is how it appears in ServiceNow, the second part is how it will appear in DevRev, and the table name in parentheses is the ServiceNow database table name\*:

* Problems (problem)
* Request Subtasks/Sn Creatorstudio Child Task (sn\_creatorstudio\_child\_task)
* [[entities/task|Tasks]]/Sn customerservice Task (sn\_customerservice\_task)
* Asset Tasks (asset\_task)
* Requests/Sc Request (sc\_request)
* Catalog Tasks/Sc Task (sc\_task)
* Stale CI Remediation (stale\_ci\_remediation)
* Cases/Sn Customerservice Case (sn\_customerservice\_case)
* Change Task (change\_task)
* Guidance Tasks/Help Guidance Task (help\_guidance\_task)
* Roster schedule entry proposal (roster\_schedule\_span\_proposal)
* Requested Items/Sc Req Item (sc\_req\_item)
* Developer Collaboration Tasks/Sn Collab Request Dev Collab Task (sn\_collab\_request\_dev\_collab\_task)
* Tickets (ticket)
* Follow On Tasks/Cert Follow On Task (cert\_follow\_on\_task)
* Knowledge Feedback Tasks/Kb Feedback Task (kb\_feedback\_task)
* KB Submission (kb\_submission)
* Escalations/Sn Customerservice Escalation (sn\_customerservice\_escalation)
* Service Tasks (service\_task)
* Guided Setup Task (gsw\_task)
* Renew Lease Tasks/Statemgmt Renew Lease Task (statemgmt\_renew\_lease\_task)
* Transfer Order Line Tasks/Alm Transfer Order Line Task (alm\_transfer\_order\_line\_task)
* Deployment Requests/Sn Deploy Pipeline Deployment Request (sn\_deploy\_pipeline\_deployment\_request)
* Change Phases (change\_phase)
* Change Requests (change\_request)
* CMDB Multisource Recomp Tasks (cmdb\_multisource\_recomp\_task)
* Asset Reclamation Requests (asset\_reclamation\_request)
* Zero Touch Refresh Fulfillment Requests/Sn Itam Ztr Fulfillment Req (sn\_itam\_ztr\_fulfillment\_req)
* Feature Tasks/Release Task (release\_task)
* Request Tasks/Sn Creatorstudio Task (sn\_creatorstudio\_task)
* New Application Tasks/Sn Creatorstudio New Application Task (sn\_creatorstudio\_new\_application\_task)
* Required Field Remediations (required\_field\_remediation)
* Alm Transfer Order Line Subtasks (alm\_transfer\_order\_line\_subtask)
* Upgrade History Tasks (upgrade\_history\_task)
* Private Tasks/Vtb Task (vtb\_task)
* Remediate Duplicate Tasks (reconcile\_duplicate\_task)
* Reclassification Tasks (reclassification\_task)
* Problem Tasks (problem\_task)
* Release Phases (release\_phase)
* Report Access Requests/Sys Report Access Request (sys\_report\_access\_request)
* Business Application Requests/Business App Request (business\_app\_request)
* Scan Tasks (scan\_task)
* Orphan CI Remediations/Orphan CI Remediation (orphan\_ci\_remediation)
* Recommended Field Remediations/Recommended Field Remediation (recommended\_field\_remediation)
* Standard Change Proposals (std\_change\_proposal)
* CMDB Data Management Task Control/CMDB Data Management Task (cmdb\_data\_management\_task)
* [[entities/group|Group]] approvals/Sysapproval Group (sysapproval\_group)
* Chat Queue Entries/Chat Queue Entry (chat\_queue\_entry)

To ease the transition from ServiceNow ITSM/CSM to DevRev, you can choose to  
import your ServiceNow data into DevRev. The import is a 1-time bulk import of  
your ServiceNow data into DevRev. Once this import is complete, several options  
are made available for that project.

### Setting up the ServiceNow connection

When creating a connection to ServiceNow, you'll need:

* Your ServiceNow instance URL (e.g., `https://yourinstance.service-now.com`)
* Valid credentials with appropriate permissions.
* ServiceNow Customer Service Management (CSM) plugin must be installed and activated on your instance.

### Project import

If you do not want to import all the objects, you can select the objects you want to import in the **Mappings required** phase.

For best results, AirSyncs should be done using an administrator account on the external source. This ensures all necessary permissions are available to complete the import successfully

And the short description field should not be empty for any of this objects. If it is empty `ServiceNow Ticket` or `ServiceNow Incident` fallback will be used.

This is because the short description field is used to create the title of the ticket in DevRev.

### Import duration and tracking

The duration of the import depends on several factors:

* **Small imports** (< 100 items): Typically complete in minutes to seconds
* **Medium imports** (100-10,000 items): May take 30 minutes to a few hours
* **Large imports** (10,000+ items with attachments): Can take several hours to days

DevRev respects ServiceNow API rate limits and automatically handles back-off and retry logic.

You can monitor the import progress in the AirSync dashboard, which shows:

* Current phase (Extraction, Transformation, Loading)
* Any errors or warnings

For large imports, consider starting during off-peak hours to minimize impact on your ServiceNow instance performance.

To import from ServiceNow, navigate to [**Settings** > **Integrations** > **AirSyncs**](https://app.devrev.ai/?setting=airsyncs) then select  
**AirSync** (or **Start AirSync** if it's your first). From there, create a new connection to a  
ServiceNow site or use an existing connection if you already have one. Once the  
connection is established, you can start the import. At this point, you are  
prompted to configure how to import your ServiceNow data.

## Periodic Sync

Periodic sync automatically keeps your DevRev and ServiceNow data synchronized on a recurring schedule. This is ideal for organizations that want to maintain ongoing bi-directional sync without manual intervention.

### Setting up periodic sync

1. Complete an initial import
2. Navigate to **Settings** > **Integrations** > **AirSyncs**
3. Locate your imported project
4. Select **⋮** > **Set Periodic Sync**
5. Configure sync settings:

   1. **Sync direction**: Choose bidirectional, ServiceNow to DevRev only, or DevRev to ServiceNow only
   2. **Frequency**: Default is once per hour

### How periodic sync works

* Runs automatically at the configured interval
* Only syncs changes since the last successful sync
* Processes new items created or updated in either system
* Updates existing items that have been modified
* Logs all sync activities in the View Report

Periodic sync requires an active connection. If the connection expires or is revoked, periodic sync will automatically pause.

### Disabling periodic sync

To stop automatic syncing:

1. Go to **Settings** > **Integrations** > **AirSyncs**
2. Locate the project
3. Select **⋮** > **Set Periodic Sync**
4. Press **Stop** button

You can still perform manual syncs after disabling periodic sync.

### Post import options

After a successful import, you have the following options available for the imported project:

* **Sync to DevRev:**

  + This option allows you to synchronize any modifications made in ServiceNow with the corresponding items previously imported into DevRev.
  + It also creates new items in DevRev for any new items created in ServiceNow after the last sync or import. This is a one-time operation.
* **Sync to ServiceNow:**

  + This option synchronizes any changes made in DevRev to previously synced ServiceNow supported items back to ServiceNow.
  + It also creates any items marked in DevRev for creation in ServiceNow. This is a one-time operation.
* **Periodic Sync:**

  + By enabling this option, you can automatically sync new changes from ServiceNow to DevRev on a periodic basis. The default frequency is once an hour.
* **View Report:**

  + This option allows you to access detailed information about the initial import and any subsequent syncs performed.
* **Delete Import:**

  + If you wish to remove the import and all items that were imported from ServiceNow into DevRev, you can use this option.
* **Edit Connection**

  + Use this option to change the connection used for any subsequent actions. It can be helpful if a connection becomes inactive or the user who established it is no longer available.

### Setting up the import recipe

A ServiceNow import is highly configurable, and the configurations for a specific import are referred to as the recipe. Here are some guidelines on what to expect:

* What type of work to create in DevRev?

  + You have the option to import ServiceNow objects as DevRev tickets and as DevRev [[features/incidents|incidents]].
* What ServiceNow types to import?

  + ServiceNow contains various types of objects. All are subtypes of Tasks or Incidents type.
  + You can select which ServiceNow objects you want to import.
* How to map ServiceNow fields to DevRev fields?

  + DevRev tries to automatically and sensibly map your ServiceNow fields to corresponding fields in DevRev, but it may prompt you on how you want to map certain fields.
  + Some stages will have to be mapped by user.

### Field mapping

DevRev automatically maps common ServiceNow fields to DevRev equivalents:

* `short_description` → Title
* `description` → Description
* `state` → Stage

  + Note: For extended task tables, ServiceNow may use table-specific state fields following patterns like `{tablename}_state` or `{partial_tablename}_state`. Examples:
  + `incident_state` for incidents table
  + `problem_state` for problems table
  + `request_state` for sc\_requests table
* `priority` → Priority
* `assigned_to` → Owned by
* `created_by` → Created by
* Custom fields can also be mapped during the import configuration

### Attachments

We support attachments on the top‑level record (ticket/incident/cases - task subtype), those will sync between systems when allowed.

* Inline attachments inside comments (in ServiceNow or DevRev) are not supported for sync and will not be synced between systems.
* Workaround: attach files to the ticket/task rather than embedding them in comments.

### Sync from ServiceNow to DevRev

After a successful import from a ServiceNow account, you can choose to sync the imported data with DevRev. This feature replicates any new items and any changes made to previously imported items from ServiceNow.

To perform a one-time sync to DevRev, follow these steps:

1. Go to [**Settings** > **Integrations** > **AirSyncs**](https://app.devrev.ai/?setting=airsyncs).
2. Locate the previously imported project.
3. Select ⋮ > **Sync ServiceNow to DevRev**.

This may override fields in previously imported items, even if they were modified in DevRev.

### Sync from DevRev to ServiceNow

After a successful import from a ServiceNow account, you can sync changes made in DevRev to the previously imported cases back to ServiceNow. Additionally, any new DevRev tickets marked for sync is created as new ServiceNow item.

To perform a one-time sync to ServiceNow, follow these steps:

1. Go to [**Settings** > **Integrations** > **AirSyncs**](https://app.devrev.ai/?setting=airsyncs).
2. Locate the previously imported project.
3. Select ⋮ > **Sync DevRev to ServiceNow**.

This may override fields in ServiceNow of previously imported items, even if they were modified in ServiceNow.

# Mark a DevRev ticket for syncing

Using the Sync to ServiceNow feature, it's possible to sync new DevRev tickets to ServiceNow. In order to sync a DevRev ticket to a specific ServiceNow type, it must be marked for syncing. During ticket creation, open the dropdown **Select Subtype**, set it to a ServiceNow type the ticket should be synced to. The format is as follows: `ServiceNow / {type}`.

For example, if you want to sync a new case to a ServiceNow account, this would show as **ServiceNow / case**.

After a DevRev work item has been marked for syncing, it's created in the specified ServiceNow account the next time the Sync from DevRev to ServiceNow runs. This can be triggered manually or automatically through a Periodic Sync. Future syncs keeps this item updated on both sides after it has been created in ServiceNow.

## ServiceNow permissions

### Required ServiceNow permissions

To successfully perform a ServiceNow AirSync, the user should have admin permissions.

**Mandatory table access (Read):**

* `sys_db_object`
* `sys_dictionary`
* `sys_choice`
* `sf_state_flow`

If permissions are denied for any of these tables, the import will fail.

**Required for data import:**

For all other tables you wish to import (incidents, tasks, [[features/accounts|accounts]], etc.), the user must have read access or that data will not be imported.

ServiceNow is highly customizable and is it possible to add which role should have access to which table. If you create a new role only for extraction and add permission to read mandatory tables, then you can import data without admin permissions.

### Recommended ServiceNow permissions for successfully importing a ServiceNow import

To successfully import a ServiceNow import, user should have admin permissions.

### Required ServiceNow roles for successfully importing a ServiceNow import

Users that we want to import as DevUsers should have following roles:

* **sn\_internal**: This tells that the user is internal to the organization and not a customer.

### Recommended ServiceNow roles for successfully importing a ServiceNow import

Recommended roles for users that we want to import as **DevUsers**:

* **admin**: This tells that the user is an administrator of the ServiceNow instance.
* **sn\_internal**: This tells that the user is internal to the organization and not a customer.
* **sn\_customerservice\_agent**: This tells that the user is an agent for the customer service.
* **sn\_customerservice\_manager**: This tells that the user is a manager for the customer service.
* **sn\_customerservice.consumer\_agent**: This tells that the user is an agent for the consumer.

For every task subtype we have agent, manager and consumer roles. If we want to assign a task to a user, they should have these roles. All other users without these roles will be imported as **RevUsers**.

## AirSync ServiceNow scope and limitations

The following is a list of AirSync ServiceNow scopes and limitations to keep in mind when performing a ServceNow AirSync. In addition to these ServceNow-specific limitations, there are also some generic AirSync scopes and limitations.

**Comments**:

* ServiceNow comment attachments are not transferred to the tickets.
* When syncing comments from DevRev to ServiceNow, attachments on comments are not transferred to ServiceNow comments.

**Updates:**

* Changes to certain custom fields in DevRev may not properly sync back to ServiceNow if they are read-only or not editable in ServiceNow.
* If there is no direct transition from the current ticket state to the next state in ServiceNow, the state in ServiceNow is not changed.

**Closing incidents**: Attempting to close incidents from DevRev may fail if ServiceNow requires mandatory closure fields (such as closure notes, resolution code, or closure category) that are not populated in DevRev. These fields must be either mapped to DevRev fields and filled, or the incident must be closed directly in ServiceNow.

**Custom Tasks and Incidents:**

ServiceNow is highly customizable. DevRev supports importing custom objects from ServiceNow. However, there are some limitations to keep in mind:

* We can't import tasks and incidents from custom objects.
* If custom objects wanted to be imported as tasks or incidents, then in ServiceNow we should create a table, that extends main Task table. If we want to create a custom incident table, then we should create a table, that contains `incident` name in it.

## Troubleshooting

### Import fails during extraction

* Verify the user has admin permissions or read access and/or write access to all mandatory tables
* Check that the ServiceNow connection is still active

### Data Sync Issues

**Items not syncing**

* Ensure the short description field is not empty for tasks/incidents
* Verify field mappings are correctly configured
* Check the View Report for specific error messages
* Confirm the connection user still has appropriate permissions

**Stage/state not updating**

* Verify there is a valid transition path in ServiceNow workflow
* Check if the target state exists in the ServiceNow workflow
* Review custom workflow restrictions in ServiceNow

**Attachments not syncing**

* Check file size limits
* Verify attachment table permissions
* Ensure sufficient storage in both systems

### Historical AirSyncs

To view currently running and previous AirSyncs from various sources, do the following:

1. Go to [**Settings** > **Integrations** > **AirSyncs**](https://app.devrev.ai/?setting=airsyncs).
2. Select the import you want to view.
3. Select the context menu (⋮) > **View Report**.

### Delete import

This deletes any content created by the import, including users and works.

An import and all the content it creates can be deleted from DevRev. This can be useful when running POCs or to change the recipe used during the import. Once an import has been deleted, all the content it created gets deleted, even if they were modified in DevRev. It's possible to import the project again after its deletion.

To delete an import and all the content it created, go to [**Settings** > **Integrations** > **AirSyncs**](https://app.devrev.ai/?setting=airsyncs), find the previously imported project, and select ⋮ > **Delete Import**.

## Related wiki nodes
- [[glossary/airsync]]

## Source
- DevRev support [[entities/article|article]] [ServiceNow AirSync](https://support.devrev.ai/en-US/devrev/article/GujEKqBQ) (ART-22008)
