---
title: Best practices for documentation that supports AI
devrev_id: ART-21916
parent_directory: Knowledge Base
translation_group: hpcQTsWr
modified_date: "2026-05-06T15:12:09.609Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/hpcQTsWr"
tags: []
top_category: Computer+ Support
wiki_match: flows/automation-priority-matrix
match_score: 0.351
last_updated: 2026-05-11
summary: "Computer works best when articles and QnAs in the knowledge base adhere to certain guidelines."
---

# Best practices for documentation that supports AI

Computer works best when [[entities/article|articles]] and QnAs in the [[features/knowledge-base|knowledge base]] adhere to certain guidelines. The old computing adage of “garbage in, garbage out” applies to AI as much as to earlier technologies. Most of these guidelines are typical for professional/technical writing, especially content that has requirements for accessibility and localization.

To enable searching through the knowledge base, Computer cuts up articles into smaller *chunks* (paragraphs and sentences). As an overarching principle, think of the various elements of an [[entities/article|article]] or QnA as modules that may be used in a variety of ways.

## Multiple mediums/modalities

* Include supporting text clearly explaining images and videos. Every image and video should have `alt` text at minimum for a variety of reasons; lengthy discussion should be in the body of the text. Images and videos (for now), are not used to train the model.
* Rather than include pictures of text, include the text itself in the body.
* Minimize the use of tables. Two-column tables can easily be represented with a description list (HTML `dl` element) or nested ordered/unordered lists.

## Structure

* Avoid long articles. Ensure tight cohesion within an article, meaning that it covers only a single topic.
* Ensure that the question in a QnA pair is properly-phrased as a question, and that the answer directly addresses to the type of question (for example, yes or no for a *yes/no* question, a procedure for a *how* question, an explanation for a *what* question).
* Include URLs of relevant articles in QnAs.
* Judiciously use pronouns (*it*, *that*), and ensure that the antecedent for pronouns is clear. Prefer using the name of the object, product, or feature.

## Chunking

* Ensure tight cohesion within paragraphs.
* Dedicate a paragraph in articles to cover common questions.
* Each paragraph should make sense when read in isolation, without the paragraphs or sections before or after it. Avoid using transition words or phrases—such as *in addition*, *next*, or *also*—to start paragraphs.

## Style

* Write your documentation in the same voice you would want your AI agent to talk to your customers.
* Consistently use approved product terminology. Avoid colloquial or internal terms and phrases, including jargon and code names.

## Source
- DevRev support article [Best practices for documentation that supports AI](https://support.devrev.ai/en-US/devrev/article/hpcQTsWr) (ART-21916)
