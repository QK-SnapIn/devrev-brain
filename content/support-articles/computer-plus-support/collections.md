---
title: Collections
devrev_id: ART-21915
parent_directory: Knowledge Base
translation_group: Xpv_jFYE
modified_date: "2026-03-17T21:18:45.737Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/Xpv_jFYE"
tags: []
top_category: Computer+ Support
wiki_match: features/conversations
match_score: 0.667
last_updated: 2026-05-11
summary: "Collections serve as the parent categories for articles within your Customer Portal, establishing a hierarchical structure for organizing and presenting content to customers."
---

# Collections

Collections serve as the parent categories for [[entities/article|articles]] within your [[features/customer-portal|Customer Portal]], establishing a hierarchical structure for organizing and presenting content to customers. By designating a collection as the parent, you create a top-level category. If you prefer to relocate this collection to another directory, you can change its parent directory accordingly.

Collections and [[features/parts|parts]] are distinct entities. Collections categorize articles on the Customer Portal, while parts represent the structure and components of a product or service.

You can nest multiple collections within a single collection to create a well-structured framework for your customer support portal and [[features/plug-widget|Plug widget]] by DevRev.

## Visibility of articles and collections

The accessibility of a collection and its articles to customers depends on their combined visibility settings. Here are a few scenarios:

* If a collection is not **Public**, none of the articles within it will be visible to customers, even if the articles are set to be **Visible to Customers**.
* If a collection is **Public**, only the articles set to be **Visible to Customers** will be publicly accessible. If an [[entities/article|article]] within the public collection is configured with visibility for **Verified Customers**, non-signed-in customers won’t be able to view it.
* If a collection is **Public** but all the articles within it are intended for internal use only, the collection itself won’t be visible to the public in the help center.

## Collection management

### Create a collection

1. Go to **Settings > Support > Article Collections**.
2. Click **+Collection** and fill in the following details:

   * Title
   * Description
   * Parent
3. Enable the **Publish Collection** option if you want your customers to see the collection and its articles in your help center.
4. Click **Create**. You will now see the newly created collection on your screen.

Similarly, if you want to add a sub-collection, click on **+Add** next to the collection and follow the same process as outlined above to create the sub-collection.

### Map an article to a collection

You can assign an article to a collection either from the collection itself or from the article's settings:

* In **Settings > Collections**, click **+ Add** next to the collection where you want to add the article, or drag and drop an article from one collection to another.
* When creating or editing an article, specify the collection to which it belongs.

### Repositioning Collections

The order of collections in your help center is determined by their arrangement in your DevRev [[entities/account|account]]. You can change the position of a collection by dragging and dropping it on the homepage or by moving it within another collection.

## Source
- DevRev support article [Collections](https://support.devrev.ai/en-US/devrev/article/Xpv_jFYE) (ART-21915)
