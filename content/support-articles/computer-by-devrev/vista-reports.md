---
title: Vista Reports
devrev_id: ART-21899
parent_directory: Vistas
translation_group: ZEO1cvTn
modified_date: "2026-02-26T10:13:09.774Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/ZEO1cvTn"
tags: []
top_category: Computer by DevRev
wiki_match: glossary/vista
match_score: 0.85
last_updated: 2026-05-11
related: ['glossary/vista']
summary: "Real-time reporting represents a paradigm shift in the way organizations access and utilize information."
---

# Vista Reports

Real-time reporting represents a paradigm shift in the way organizations access and utilize information. In the realm of real-time reporting, the emphasis lies not just on the speed of data delivery but also on maintaining a continuous and seamless contextual flow. By enabling instant access to live data, real-time reporting ensures that decision-makers are not only kept abreast of the latest developments but can also interpret these updates within the broader context of their operations.

This immediacy eliminates the need for constant context-switching, allowing stakeholders to stay focused on their [[entities/task|tasks]] without interruptions. Whether tracking key performance indicators, monitoring operational metrics, or analyzing customer behavior, real-time reporting allows organizations to maintain a consistent context, enabling a more accurate understanding of their current state and facilitating proactive responses to emerging trends or challenges.

With [[glossary/vista|Vista]] Reports, you can retain the context of the vista you are working with and bring in data from other sources as well.

## Discover

To get started, click the three dots on a vista. The following options are available:

* Create New Report
* View Past Reports: Created by me or shared with me

You can also [[features/search|search]] for reports and find more on the **Explore** page.

### Create

You can create your own reports by adding a name, description, and creating widgets. Here, you'll also be able to preview your report and make any necessary adjustments before finalizing it.

## Widget builder

With the widget builder, you can create custom widgets for your vista reports. You can define the widget's data source, construct measures, dimensions, and pick a suitable visualization. The widget builder offers a range of tools and options to help you create the ideal widget for your report.

Widgets represent the building blocks of DevRev Dashboards. They are the leaf-level data visualizations which are composed together to form a dashboard.

**Data source**

A data source specifies the backing data that powers the widget. You [[glossary/don|don]]’t need to worry about the data source, as it’s all auto-populated.

**Measures & Dimensions:**

Measures & Dimensions provide additional details about the required columns from the base SQL-constructed view.

* Each column that needs to be [[entities/part|part]] of the visualization in the chart must be specified as either a measure or a dimension.
* Columns specified as measures are meant to represent measurable or numerical types of data. These columns are most likely to be placed on the y-axis in a chart. For example, `number_of_tickets`.
* Columns specified as dimensions are meant to represent categorical, groupable, or date-type data. These columns are most likely to be placed on the x-axis in a chart. For example, `stage`.

**Visualization**

A visualization specifies the type of chart along with the related metadata.

### Auto-visualization generator

The auto-visualization generator is an AI-powered algorithm designed to generate a default visualization based on the number and type of selected measures and dimensions. The algorithm determines the best visualization and handles scenarios where the user has not specified a visualization type or when the selected data does not align with a specific chart type. It ensures that a meaningful default visualization is provided to the user, enhancing the user experience and ensuring data visibility even in ambiguous situations.

**Visualization types**

Visualization type refers to the type of chart used to render the widget. Supported types are: `metric tile` , `table`, `bar`, `line`, `column`, `table`, `donut`, `pie`, `stacked bar` , and `stacked column`.

![visualization types](don:core:dvrv-us-1:devo/0:artifact/4100397)

### Preview

The **Preview** button is an essential tool that helps you visualize your inputs before finalizing them. By clicking this button, you can see a real-time representation of the data or elements you have chosen. This feature provides you with an [[glossary/opportunity|opportunity]] to review and make any necessary adjustments to ensure everything is perfectly set up. It serves as a preventive measure to help avoid mistakes or misunderstandings, ultimately saving you time and effort in the long run. Utilize the **Preview** button effectively to maintain the quality and accuracy of your reports.

### Filters

* **Vista Filters**: Most or all of the filters from your vista will be transferred to your widget definition. If any filters are not carried over, a message will indicate the reason, and you will have the option to add the missing vista filters to your widget filter definition.
* **Widget Filters**: These filters are for your widget definition and include all filters from the vista, as well as other objects.

The filters and dimensions are interlinked. To have filterable values, you must select them in dimensions as well.

### Save

Add measures, dimensions, and filters. Experiment with arranging them, preview your changes, and remember to **Save** your widget. This ensures the widget appears on the dashboard.

### Custom fields

You can also create reports based on custom fields by creating them via Object [[features/customization|Customization]]. You’ll be able to utilize these custom fields in report generation, as they can be used in measures, dimensions, and filters.

### Cross-entity joins

DevRev’s data model is a reflection of Computer's powerful Memory. Leveraging the data model is key to getting answers to key questions and obtaining strategic insights. Here’s the data model you’d need for constructing widgets and answer questions around a vista. For example, ticket-based vista.

You don’t have to worry about these join paths, as DevRev identifies the entity relationships and populate them for you. You just need to search for the actual field you are looking for, and the join paths are identified for you.

![data model](don:core:dvrv-us-1:devo/0:artifact/4100400)

### Edit

You can enter *Edit* mode by clicking the ⚡ button on your dashboard main page and edit the following:

* Dashboard layout: Move your widgets around through a drag-and-drop UI, utilize the canvas-like interface to arrange your widgets. You can also resize widgets.
* Add section: You can add a section and move widgets into the section.
* Widgets: Edit a widget from the ✏️ icon. This will take you into the widget builder.

### Share

Share reports/dashboards by clicking the ⚡ button on your dashboard main page. Based on whether you have access, you can share with team members.

## Authorization (MFZ)

For Authorization ([[features/mfz|MFZ]]) related information, refer to [[support-articles/computer-by-devrev/access-control-overview|Vista Reports Authorization]].

## Related wiki nodes
- [[glossary/vista]]

## Source
- DevRev support [[entities/article|article]] [Vista Reports](https://support.devrev.ai/en-US/devrev/article/ZEO1cvTn) (ART-21899)
