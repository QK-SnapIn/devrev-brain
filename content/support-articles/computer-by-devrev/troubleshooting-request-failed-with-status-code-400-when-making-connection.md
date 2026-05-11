---
title: Troubleshooting "Request Failed with Status Code 400" When Making Connection
devrev_id: ART-20106
parent_directory: AirSync
translation_group: 70leOhpi
modified_date: "2025-12-17T07:29:08.812Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/70leOhpi"
tags: []
top_category: Computer by DevRev
wiki_match: features/_minor-features
match_score: 0.351
last_updated: 2026-05-11
summary: "When integrating external systems with DevRev, you might encounter a \"Request failed with status code 400\" error after filling out the connection form."
---

# Troubleshooting "Request Failed with Status Code 400" When Making Connection

When integrating external systems with DevRev, you might encounter a "Request failed with status code 400" error after filling out the connection form. This [[entities/article|article]] will help you understand common reasons for this error and how to resolve them.

## Common Reasons for "Request Failed with Status Code 400"

1. **Incorrect Subdomain Format:**

   1. Some connections require both the subdomain and the full domain (e.g., `<your-company-name>.atlassian.net`), while others only need the subdomain (e.g., `<your-company-name>`) although in both cases the field will require only "subdomain".
   2. **Recommendation:** If you receive a 400 error, try both formats for the subdomain field.

      1. **Example for Jira:** Try `<your-company-name>.atlassian.net` or just `<your-company-name>`
      2. **Example for ServiceNow:** Try `<your-company-name>.service-now.com` or just `<your-company-name>`
   3. **Note for GitHub Snapin:** For GitHub, you need to provide your **organization name** in the subdomain field.
2. **Typos, Leading/Trailing Spaces, or Incorrectly Copied PAT Token:**

   1. Even small errors can cause connection failures.
   2. **Recommendation:**

      * Double-check all fields for typos.
      * Ensure there are no leading or trailing spaces in any of the input fields.
      * Verify that you have correctly copied and pasted your Personal Access Token (PAT).
3. **Invalid or Insufficient Personal Access Token (PAT) Permissions:**

   1. Your PAT might not have the necessary permissions or privileges to establish the connection.
   2. **Recommendation:**

      * Review the required permissions for the external system you are trying to connect to DevRev.
      * Generate a new PAT with the correct permissions, if necessary.
      * Consult the external system's documentation for details on PAT requirements.

## Source
- DevRev support article [Troubleshooting "Request Failed with Status Code 400" When Making Connection](https://support.devrev.ai/en-US/devrev/article/70leOhpi) (ART-20106)
