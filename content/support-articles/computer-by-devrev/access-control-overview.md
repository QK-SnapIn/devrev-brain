---
title: Access control overview
devrev_id: ART-21834
parent_directory: Access control
translation_group: H9YTDYQY
modified_date: "2026-04-18T04:32:29.81Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/H9YTDYQY"
tags: []
top_category: Computer by DevRev
wiki_match: overview
match_score: 0.564
last_updated: 2026-05-11
summary: "Access control in DevRev is a system that authorizes an actor to perform actions on different targets within the application."
---

# Access control overview

Access control in DevRev is a system that authorizes an actor to perform actions on different targets within the application. In this context, an actor is any entity that interacts with the app, such as an organization member, a customer, a system user, or a service [[entities/account|account]].

When an actor attempts to carry out an action, such as creating an [[entities/issue|issue]], the access control system checks the actor's role to determine if the actor has the necessary privileges to perform the desired action.

## Privilege determination

A role is a defined grouping of access privileges that determines what actions a user can perform on different objects. These objects can include [[features/stock-objects|stock objects]] like issue, [[entities/ticket|ticket]], etc., custom objects, and their subtypes. By assigning a role to a user, you grant them specific permissions—such as read, write, update, or delete- enabling access across these objects.

The process of checking access is as follows:

1. Fetch all the user's [[support-articles/computer-by-devrev/groups|groups]].
2. Fetch [[support-articles/computer-by-devrev/roles|roles]] associated with the user directly or roles associated with the [[entities/group|groups]] the user is a member of.
3. For each of these roles, look for the object for which user access is needed to be checked. Say, [[features/tickets|Tickets]].
4. Look at each role's ticket configuration to understand the access the user has on the object.

   ![image.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/9338902&key=76947b995a57acb7a0c8c3491516b2a1d9e4fd6cb867db7a6c5ee4d2302d1a8d)

   **Connections between users, groups, roles, and objects**

   ![image.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/9953560&key=bf822309418950a8e27338c1c0fdab0bc5f669b4c0db7dab7cb953f6bac82866)

If users attempt an unauthorized action, they'll see a message stating, *You are not authorized to perform this action.* Relevant buttons may be inactive. Users can contact their organization's admins to request access.

![inactive buttons](don:core:dvrv-us-1:devo/0:artifact/4099817)

## Grant access permissions

Users are granted access permissions to dashboards or reports through [[features/mfz|MFZ]] policies and sharing.

### MFZ policies

Use of MFZ policies facilitates the need to grant access to a wider [[entities/group|group]] of users.

An org admin has permission to define and enable roles, in whatever combination, that will give user groups permission to perform various operations on dashboards/reports. Out of the box, the following roles are enabled for the predefined user groups:

* **Admins role**

  ![image.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/9337924&key=ba5a0d07f7a9696eab78ea39dd17ba374319f90c510031272d5fe1df8bfc2fe6)
* **Platform Users role**

  ![image.png](https://app.devrev.ai/api/gateway/internal/artifacts.download?id=don:core:dvrv-us-1:devo/0:artifact/9953530&key=7538314ebb5527784172821ad759b0a3625e536565f18d6029470c618482a409)

  By default, platform users have the following permissions:

  + Create dashboards or reports.
  + Read, update, and delete their own dashboards or reports.
  + Create datasets.
  + Read, update, and delete their own datasets.

Platform users do not, by default, have permission to read any datasets besides their own. Admins are responsible for granting read permissions to all or a subset of datasets, which platform users can then utilize in building dashboards or reports.

### Sharing

The share functionality allows dashboard or report editors to grant read or update permissions to other users.

1. Select **Share** from the actions drop-down.
2. [[features/search|Search]] for the desired user, assign them a role (Editor or Viewer), then click **Share**.

## Vista privileges

Two objects power [[glossary/vista|vista]] reports: dashboards and datasets. Dashboards represent the view, while datasets represent the actual underlying data. A user must, at a minimum, have access permissions to dashboards in order to perform any meaningful operations on vista reports. Below is a list of possible operations:

* **Read**: View a dashboard or report. Dashboard `read` permissions are required for a user to view a dashboard or report.
* **Create**: [[features/build|Build]] a dashboard or report. A user must have dashboard `create` permissions and dataset `read` permissions to create a dashboard or report.
* **Update**: Modify an existing dashboard or report. A user must have dashboard `update` permissions and dataset `read` permissions to modify a dashboard or report.
* **Share**: Allows a user to share an existing dashboard or report with other users. A user must have dashboard `update` permissions to share a dashboard or report.

## Source
- DevRev support [[entities/article|article]] [Access control overview](https://support.devrev.ai/en-US/devrev/article/H9YTDYQY) (ART-21834)
