---
title: Object customization
devrev_id: ART-21854
parent_directory: Computer by DevRev
translation_group: 2it-yKhx
modified_date: "2026-03-16T11:53:29.253Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/2it-yKhx"
tags: []
top_category: Computer by DevRev
wiki_match: features/customization
match_score: 0.85
last_updated: 2026-05-11
related: ['features/customization']
---

# Object customization

DevRev powers your organization with the ability to customize DevRev objects for your organization's needs. You can add custom fields to the objects along with the pre-existing fields or add new subtypes to the objects which helps you extend an object's capabilities.
Objects are the core entities in DevRev that represent the data you work with. For example, issues, opportunities, contacts, and accounts are objects in DevRev. You can read more about how identity, parts, and work items work in [[support-articles/computer-by-devrev/core-concepts|core concepts]].
Here's how objects and subtypes work in DevRev:

![Object Customization Diagram](don:core:dvrv-us-1:devo/0:artifact/4099910)

**Key features**:

* Create custom object records: Easily create records for custom objects directly from the + button.
* Search: Use cmd+K to quickly find and access your custom object records.
* Association with stock and custom objects: Map custom objects to stock objects like tickets or contacts, as well as other custom objects.

Object customization is available only for the following:

* [[support-articles/computer-plus-build/issues#attributes|Issues]]
* [[support-articles/computer-plus-support/tickets#attributes|Tickets]]
* [Opportunity](https://support.devrev.ai/devrev/article/ART-21830#opportunity-attributes)
* [Account](https://support.devrev.ai/devrev/article/ART-21830#account-attributes)
* [Contact](https://support.devrev.ai/devrev/article/ART-21830#contact-attributes)
* [[support-articles/computer-by-devrev/parts-trails#attributes|Parts]]

Adding custom fields can be done by workspace admins only. Members of your organization can only view the custom fields and subtypes.

To get started with object customization, go to [**Settings** > **Object customization**](https://app.devrev.ai/?setting=object-customization).
Here you can view all the existing objects and their subtypes. You can also check the objects that are no longer in use by going to **Show deprecated objects**.

## Add a new field to an object or a subtype

1. Select the object or subtype you want to add to the custom field.
2. Clicking the **+ New field** button takes you to the edit mode where you can fill in the following details:

   * **Field name**: Provide a descriptive and clear name that tells you what it's about.
   * **Field type**: Select what kind of custom field it is from the dropdown.
     These are the following field types and their value definitions:

     + **Text**: You can add unformatted text to this field. For example, "enter your name"
     + **Rich text**: You can add formatted text to this field. For example, ```` **Tile** > Quote ```code block`` 1. ordered list ````
     + **Number**: You can add numbers in this field.
     + **Double**: You can add decimal numbers in this field.
     + **Boolean**: You can add input which is either 0 or 1. When you add this input field the user can toggle on or off this option.
     + **Dropdown**: You can select the options from the dropdown. Add options using **Dropdown options** > \**+ Add* in the value definitions section.
     + **Timestamp**: You can add the date and exact time in this field.
     + **Date**: You can select a date in this field. For example, "Date of bug identified: 19/07/2024".
     + **Part**: Select the part to which this object belongs. It could be an enhancement, feature, capability, runnable, linkable, or product.
     + **Dev user**: Select one or multiple users from the dropdown.
     + **Customer**: Assign the object to an existing customer workspace.
     + **Account**: Assign the object to a customer account.
     + **Workspace**: Assign the object to a workspace.

       - **Value definitions**:

         * **Allow multiple values**: Toggle this on if you want users to add multiple values instead of just one.
         * **Required field**: Toggle this on if you want to make it a required field. Required fields will have a red star which indicates that to create an object, this field needs to be filled.
         * **Default value**: Add a default value in the input so that it's not empty. Users can change this value later.
         * **Placeholder text**: Add a placeholder text that will be visible to the users before they enter an input.
         * **Group name**: You can use a group name to create a group accordion for the chosen attributes.
   * **Field visibility**: Choose how you want the field to be visible to users.
   * **Field actionables**: Select actions that you can perform after creating a field such as grouping, filtering, and sorting.
   * **Tooltip**: Add information about the field which will be visible when hovered on the field.
   * **Description**: Add some information about why you added this field. This is only visible to you.
3. Click **Save to draft**. These fields can be reviewed and then published by clicking **Publish changes**.
4. Review the changes and click **Publish changes** once you are ready.
5. Refresh the page to see the changes in published mode. You can't make changes in this mode.

To edit or delete a custom field, click the ⋮ icon next to the field. You'll see two options: **Edit** and **Delete**. Click **Edit** to enter edit mode and make changes. This mode displays all the recent changes you have made. Changes persist locally, meaning they will remain as you navigate around the app.
However, if you refresh or close and reopen the app, these changes will vanish. If you choose to delete the field, ensure you won't lose any important data before proceeding.

![add a custom field](don:core:dvrv-us-1:devo/0:artifact/4099911)

## Add a new subtype

You can add a new subtype to an existing object.

1. Click **+** on the right side of **Objects**. A **New subtype** popup will appear.
2. Provide a name and description and select which object this belongs to. Click **Proceed**.
3. You can now customize this subtype as per your wish. Click **Edit** in the top right corner.
4. Add new fields that you need.
5. Publish the subtype to make it live.

To delete the subtype, ⋮ next to **Edit** then **Deprecate subtype**.

* Existing instances linked to this subtype remain unchanged. However, to edit them, users must restore the subtype. You can restore the subtype by going to **Show deprecated objects** and clicking ⋮ > **Restore subtype** on the selected subtype.
* Users won't be able to create new instances using this deprecated subtype.

## Related wiki nodes
- [[features/customization]]

## Source
- DevRev support article [Object customization](https://support.devrev.ai/en-US/devrev/article/2it-yKhx) (ART-21854)
