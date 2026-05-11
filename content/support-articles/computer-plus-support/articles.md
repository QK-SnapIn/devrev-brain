---
title: Articles
devrev_id: ART-21914
parent_directory: Knowledge Base
translation_group: CsHTBzn7
modified_date: "2026-02-26T06:43:22.488Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/CsHTBzn7"
tags: []
top_category: Computer+ Support
wiki_match: entities/article
match_score: 0.933
last_updated: 2026-05-11
related: ['entities/article']
---

# Articles

An article is a document containing essential information about your company’s products, services, and processes. The objective is to assist customers in resolving common queries by referring to the information in articles, enabling them to find solutions independently rather than relying on ticketing or speaking to agents.

Users with edit rights can create new articles and modify existing ones.

## Article management

### Create an article

To create a new article, do the following:

1. Go to [**Settings** > **Support** > **Knowledge Base**](https://app.devrev.ai/?setting=knowledge-base%2Farticles) and click **+Article**. Give the article a title and description.
2. Select one of the following options:

   * Write a new article using the rich-text editor.
   * Add a link to an existing article hosted on a website. When selected, this link should redirect to the source in a new browser tab, ensuring view access to the document link.
   * Upload a file (PDF or MS Word document). Selecting a PDF should open the source in a new browser tab, while selecting a Word file should download the source, requiring the user to open it in the MS Word application.
3. If you are writing a new article, specify additional settings for the article:

   * **Part** (required): Define the feature or capability the article addresses.
   * **Owned by** (required): Assign a singular point of contact responsible for the article, aiding in management and ownership.
   * **Status**: Indicate the current stage of the article.
   * **Collection**: Categorize the article under a topic/theme in your customer portal.
   * **Visible To**: Decide whether the article should be visible to all customers or only verified customers.
4. Click **Create** and select whether you want to **Create** an article in draft mode, **Submit for review**, or **Publish**.

To ensure that the article is visible to your users, the **Status** of the article must be *Published* and the user group must be indicated in the **Visible to** field.

### Edit article content and settings

To update the content or settings of an existing article, do the following:

1. Go to [**Settings > Support > Knowledge Base**](https://app.devrev.ai/?setting=knowledge-base%2Farticles) and select the article you want to edit. The article opens in an additional window on top of the knowledge base view.

Select the full screen mode icon to expand the article view.

2. Click the pen icon in the top right corner of the article to make the article editable.
3. Make the necessary changes and click **Save** or **Publish**.

   * If you **Save** the article, the changes are saved as a new draft version. Edits are not be reflected in the current published version if one exists.
   * If you **Publish** the article, a new version is created and published, making the changes visible to your customers.

Once saved or published, the article is updated accordingly.

### Delete articles

To delete an article from the knowledge base, click the bin icon next to the article in the main window. You can also select multiple articles to delete simultaneously.

You must have admin privileges to delete an article.

### Bulk change options

In the main knowledge base view, you can select multiple articles to delete articles in bulk or to modify article settings, such as transitioning multiple articles from *Draft* to *Published* stage.

## Status settings

* *Draft*: The article isn't ready to be released to the public. You can make edits at this stage.
* *Published*: The article has already been released to the public.
* *Archived*: Articles that are outdated and no longer required can be removed by archiving them.

## Visibility settings

### Article visibility

To control who can view the articles, open the **Visible to** menu. This displays all external groups that the article can be shared with. By default, the following groups are available:

* **Customers**: Allows public access without verification.

  Public access requires the public portal to be enabled. If the public portal is not enabled, only verified (signed-in) customers can view the article.
* **Verified Customers**: Limits visibility to customers signed in to the customer portal.
* **Customer Admins**: Restricts access to a subset of verified customers in the **Customer Admin** group. Membership in this group is managed through [**Settings > Customer Management > Group > Customer Admin**](https://app.devrev.ai/?setting=customer-groups%2Fgroup-default7).

  If an article is for internal use only, leave the **Visible to** field blank.

### Storage limits for articles

* There is no limit to the number of articles that can be created in the DevRev knowledge base.
* Each article is stored as an artifact, with a maximum size of 250 MB per artifact.

### Enable customer access for your knowledge base

To make your help center, including your knowledge base, accessible to the public, under [**Settings > Plug & Portal > Portal Settings**](https://app.devrev.ai/?setting=portal-settings%2Fconfiguration), go to **Help Center** and enable **Help Center** and **Public Portal**.

### Share an article

Once you've created an article, you have two options to share it:

* Use **Copy external link** to share with your customers, allowing them to access the article directly.
* Use **Copy internal link** to share with your internal organizational team members.

The ability to view the article depends on the settings for **Visible to** and **Status** that have been configured.

* If you are sharing an external link with non-signed-in customers, the article should be visible to customers. If the **Visible to** option is set to **Verified Customers**, only signed-in customers are able to view the article.
* When sharing an external link with customers, the article status should be *Published*. If it is in *Draft* mode, they won’t be able to view it.

## Article Formatting

When you’re creating a new article or editing an existing article, formatting options are displayed. While inputting text, type the slash command `/`. This opens a drop-down menu of formatting options. The drop-down menu offers typical options like font styling and alignment, as well as special elements like adding hyperlinks, code, quotes, callouts, tables, and video embeds. DevRev Knowledge Base supports embedding videos directly in articles. Use the `/` slash command, select Video Link, paste your video URL (YouTube, Loom, Vimeo, Wistia supported), and save.

When you select text in the editor, a formatting bar appears above the text. This bar includes a subset of formatting options from the top pane, along with the **Ask AI** feature, which can rephrase, lengthen, shorten, or correct the text in articles.

DevRev knowledge base articles can include a table of contents on the customer portal. Use the slash command and header options to label key topics, which form the table of contents on the customer portal.

You can filter articles using various criteria. Click the **+** icon to reveal additional criteria. You can also sort, group, and customize the displayed columns.

## Article version management

Every time an article is updated, a new version is saved. You can track who made updates, when, and restore older versions if needed.

View and restore previous versions:

1. Open the article and click the 3-dot menu at the top right.
2. Select **Versions**.
3. Click **Restore version** to revert to a previous version.

## Article templates

Article templates help maintain consistency and save time during article creation.

### Create a template

1. Go to [**Settings > Templates**](https://app.devrev.ai/?setting=record-template) and click **+ Create**.
2. Enter a name and description, then select **Article** as the object type.
3. Click **Next** and set up the template structure.

### Use a template

1. Go to [****Settings** > **Support** > **Knowledge Base****](https://app.devrev.ai/?setting=knowledge-base%2Farticles) and select **View Templates**.
2. Select a template and click **Use Template**.

### Edit a template

1. Go to [**Settings** > **Customization** > **Templates**](https://app.devrev.ai/?setting=record-template).
2. Locate the template and click the **3-dot menu** under the **Action** column.
3. Click **Edit**, make your changes, and click **Publish**.

## Content blocks

Content blocks let you create reusable content—including text, images, tables, and embedded videos—which can be inserted into multiple articles. Updates to a content block automatically reflect in every article where it's used.

### Create a content block

1. Go to [**Settings** > **Support** > **Content Blocks**](https://app.devrev.ai/?setting=content-block) and click **Create Content Block**.
2. Enter a name and description, add the required content, and click **Create**.

### Insert a content block

1. Open or create an article.
2. Type the slash command `/` and select **Content Block**.
3. Choose from the list and click **Use content block** to insert.

### Modify a content block within an article

1. Hover over the content block and click the 3-dot menu.
2. Select **Unlink** to edit the content independently for that specific article.

## Edit an existing content block

1. Go to [**Settings** > **Support** > **Content Blocks**](https://app.devrev.ai/?setting=content-block).
2. Select the block, click **Edit**, make your changes, and click **Update**.

## Article approval

The article approval process enables efficient collaboration between the Drafter, Approver, and Publisher roles.

Roles:

* *Drafter* and *Approver*: Can draft articles, submit for review, approve articles (if assigned), and cancel ongoing approval processes.
* *Publisher*: Can publish articles (with or without approval) and has all drafter & approver rights.

By default, all users have drafter and approver rights but not publisher rights. To assign publisher rights, go to **Settings > User Management > Internal Groups > Publisher Group > + User**.

Contact your DevRev representative to enable the article publisher group.

Admin users can perform all drafter, approver, and publisher functions, including article deletion.

### Submit an article for review

1. Create an article and click the **Create** drop-down.
2. Select **Create and submit for review**.
3. Add reviewers to the approval process, who receive notifications and are tagged in the **Discussions** tab.

Article approval is available only for articles created natively within DevRev.

### Review an article

1. Open the article and locate the **Review** icon at the top right.
2. Choose to either **Request Changes** or **Approve**.
3. If requesting changes, provide feedback in the placeholder.

An article is considered approved when all reviewers have approved it.

### Publish an article

1. Open the article and locate the **Publish** icon at the top right.
2. Click **Publish** to make the article available to customers.

### Status and stages

* Status options:

  + *Draft*: Internal only, not visible to customers
  + *Published*: Visible to customers via the customer portal
* Stage options:

  + *No Stage* (default): No approval process started
  + *In Review*: Submitted for review
  + *Ready to Publish*: All reviewers have approved

## Article analytics

Article analytics in DevRev provides a customized prebuilt dashboard to assess whether customers can find relevant articles to address their queries.

Access analytics under [**Settings** > **Support**> **Article Analytics**](https://app.devrev.ai/?setting=article-analytics?dashboardId=don%3Adata%3Advrv-us-1%3Adashboard%2FjoDZWGmRDo&dashboardToken=ZGV2cmV2LW9hc2lzNj6Q_7q4mkqFSM1mEwOl_IRS3DO5PR7v1QwJzTTk60XbZ0Rfwmo_Tk3a2nuwmFljyS51IwmOlQCbeSHhCQsY5Di0UuIX3w3-A16NG3LUh9fVeMqV_rv2vuk1Jy9YWzJ_cfMyN3giA39F1YWzuLKUHhBa1HvWgBsmDA%3D%3D&dashboardTabId=article-analytics-dashboard&record_date=%7B%22presetType%22%3A%22last_n_days%22%2C%22presetValue%22%3A30%2C%22type%22%3A%22preset%22%7D).

The dashboard shows the effectiveness of your knowledge base for both customers and internal employees with these metrics:

* Viewership: Total views, unique views, viewership by user type, viewership by channel
* Engagement: Average time spent on an article
* User feedback: Upvotes and downvotes

To view specific metrics, adjust the time range using the **Date** filter at the top left of the section.

## Related wiki nodes
- [[entities/article]]

## Source
- DevRev support article [Articles](https://support.devrev.ai/en-US/devrev/article/CsHTBzn7) (ART-21914)
