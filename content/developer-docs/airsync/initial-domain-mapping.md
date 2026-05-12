---
title: Initial domain mapping
type: developer-doc
status: stable
source: developer.devrev.ai
category: airsync
source_url: https://developer.devrev.ai/airsync/initial-domain-mapping
last_updated: 2026-05-11
summary: "Initial domain mapping is a process that establishes relationships between external data schemas and DevRev's native record types."
---

# Initial domain mapping

Development Guide

# Initial domain mapping

Initial domain mapping is a process that establishes relationships between
external data schemas and DevRev's native record types.
This mapping is configured once and then becomes available to all users of your snap-in,
allowing them to import data while maintaining semantic meaning from their source systems.

The initial domain mapping is installed automatically by the SDK when a snap-in version change is detected.
It is triggered on the first stateful event (such as metadata extraction) after the version update.
Developers must pass the `initialDomainMapping` parameter to `spawn()` for this to work:

```
import initialDomainMapping from '../external-system/initial_domain_mapping.json';

await spawn({
  event,
  initialState,
  baseWorkerPath: __dirname,
  initialDomainMapping,
});
```

## [JSON structure](#json-structure)

The `initial_domain_mapping.json` file has the following top-level structure:

```
interface InitialDomainMapping {
  starting_recipe_blueprint?: object; // Optional: A recipe blueprint object to pre-create
  additional_mappings?: object;       // Optional: Contains record_type_mappings, format_version, devrev_metadata_version
}
```

A typical file looks like:

```
{
  "additional_mappings": {
    "record_type_mappings": {
      "todos": { ... },
      "users": { ... }
    },
    "format_version": "v0.2.0",
    "devrev_metadata_version": 13
  }
}
```

The `record_type_mappings` object maps external record type keys to their `default_mapping` and `possible_record_type_mappings` configurations.

For a complete example, see the [initial\_domain\_mapping.json](https://github.com/devrev/airdrop-template/blob/main/code/src/functions/external-system/initial_domain_mapping.json) file in the starter template.

## [Approaches](#approaches)

You can create initial domain mappings using two methods:

1. **Chef UI**: Interactive web interface for comprehensive mapping creation
2. **Model Context Protocol (MCP)**: AI-assisted mapping creation for developers (experimental)

Choose the Chef UI for manual control or use MCP for rapid prototyping with AI assistance.
MCP is an experimental feature and works locally without requiring a sync to be created.

The two approaches work on the same format of initial domain mapping file, allowing you to use them together.

For AI-assisted mapping creation, see the [Model Context Protocol integration guide](https://developer.devrev.ai/airsync/mcp).

## [Chef UI setup](#chef-ui-setup)

### [Prerequisites](#prerequisites)

* Snap-in is set up, deployed, and activated.
* An import has been created and is in the mapping stage.

It's also required that you have the DevRev CLI authenticated appropriately.
This can be done either with `devrev profiles authenticate -e prod -o <your_org_slug> -u <your_email>`
or by running `make auth` in your snap-in repository.

### [Add your token as an environment variable](#add-your-token-as-an-environment-variable)

Obtain a PAT-token from the **Settings** > **Account** tab of the org where you deploy your snap-in,
and export it as `DEVREV_TOKEN`.

You can also run the following command if you are authenticated with the CLI:

```
export DEVREV_TOKEN=$(devrev profiles get-token access)
```

### [Initialize the context of the sync](#initialize-the-context-of-the-sync)

To allow the CLI to work in the context of that sync, you need to provide its identifying properties in an environment variable.
The recommended method is to run:

```
chef-cli ctx switch --env prod
```

This prints the list of AirSync imports in the org. Select the one you want by running:

```
eval $(chef-cli ctx switch --env prod --id <import_id>); chef-cli ctx show
```

If this method doesn't work, you can manually export the variable (replacing the values based on the logs of your running import):

```
export AIRDROP_CONTEXT='{"run_id":"1","mode":"initial","connection_id":"x","migration_unit_id":"1234","dev_org_id":"DEV-XXXX","dev_user_id":"DEVU-1","source_id":"07-16","source_type":"ADaaS","source_unit_id":"x","source_unit_name":"x","import_slug":"x","snap_in_slug":"x"}'
```

Or you can use the interactive helper of the CLI:

```
eval $(chef-cli ctx init); chef-cli ctx show > ctx.json
```

### [Use the Chef UI](#use-the-chef-ui)

```
chef-cli configure-mappings --env prod
```

If your org is not in `US-East-1`, you h ave to override an environment variable to make sure the tool reaches the right server. For example:

```
ACTIVE_PARTITION=dvrv-in-1 chef-cli configure-mappings --env prod
```

The options are: `dvrv-us-1`, `dvrv-eu-1`, `dvrv-in-1`, and `dvrv-de-1`.

The first function of the Chef UI is to assemble a *blueprint* for a concrete import running in the test-org, allowing the mapping to be tested out and evaluated.
After it is used for the import, the mappings become immutable, but the Chef UI offers a button to make a draft clone, which can be edited again for refinements.

### [Continue to initial domain mapping](#continue-to-initial-domain-mapping)

When you are done, you should have the chef-cli context set up and have the Chef UI running in your browser.
You can now use the Chef UI to create initial domain mappings.

## [Use the Chef UI to create initial domain mappings](#use-the-chef-ui-to-create-initial-domain-mappings)

Launch the Chef UI using

```
chef-cli configure-mappings --env prod --idm path/to/initial_domain_mapping.json
```

The Chef UI modifies the provided initial domain mapping file that must be embedded in your extractor. This defines the options that the end-user sees when they are mapping the data.

Initial domain mappings provide two key configuration capabilities:

* **Multiple mapping options**: The developer can choose how external record types map to DevRev records (for example, external *task* can map to either *issue* or *ticket*).
* **Category-based defaults**: Mappings can apply to entire record type categories, automatically handling new record types.

### [Map record types and fields](#map-record-types-and-fields)

Use the Chef UI to map record types and fields.
The UI displays the external record types you defined in external domain metadata and allows you to map them to DevRev objects.
Map one record type at a time, ensuring you map all required fields and as many optional fields as possible.

#### [Mapping as custom object](#mapping-as-custom-object)

The system allows importing record types and categories as custom objects. To achieve this you have to select `new_custom_object` when mapping the record type. For each external record type mapped as a custom object, a new custom **Leaf type** will be defined in DevRev and a **Subtype** will automatically be created. For more details on customization concepts, please refer to the
[Object Customization](https://developer.devrev.ai/guides/object-customization) and [Custom Objects](https://developer.devrev.ai/guides/custom-objects) documentation.

The field mapping works the same as for the stock DevRev types, with the difference being that there are significantly fewer fields to map. All the unmapped fields of the external record type will be created as custom fields.

### [Specify fallback mappings](#specify-fallback-mappings)

For some required DevRev fields a fallback is required.

The fallback you choose is used on item creation if the extractor doesn't provide a value for the required DevRev field.
This is useful for fields that are required by DevRev but optional in the external system.

### [Apply the blueprint](#apply-the-blueprint)

Apply the mappings to the in-progress import using the "Apply to import" button, and verify the imported data is as expected in DevRev.

### [Merge configurations](#merge-configurations)

Using the "Merge to initial mapping file" button, you are able to select the mappings applied to specific record types in the current import, and copy them into the initial domain mapping file you provided with the `--idm` flag.

If the initial domain mapping file doesn't exist yet, Chef will create it. If it exists, it must be a valid file created by the MCP or the mapping UI.

To create multiple mapping options (mapping to multiple possible DevRev types and letting the end user decide) for a record type, repeat this process:
Create a new import, map the record types and fields, then merge the mappings to the existing initial domain mapping file.

Chef CLI versions prior to 0.10.0 allowed the initial domain mapping to be directly installed into the given org from the mapping UI, and thus apply to all new imports.
This workflow is no longer supported. Instead the mapping UI will directly edit the file provided under `--idm`, and it is this file that has to be embedded in the snap-in for the initial domain mappings to take effect.

### [Advanced configuration](#advanced-configuration)

You can provide a local metadata file for enhanced functionality:

```
chef-cli configure-mappings --env prod -m metadata.json
```

This enables:

* Raw jq transformations using external fields as input (experimental)
* Example input data for testing transformations

The local metadata file is not validated against the snap-in submission.

### [Test an import with initial mapping using the in-app UI](#test-an-import-with-initial-mapping-using-the-in-app-ui)

Once the initial mappings are prepared, any new import in the org (with the same snap-in slug and import slug) where they are installed will use them.
The end-users can influence the recipe blueprint that gets created for the sync unit through the mapping screen in the UI, where they can make record-type filtering, mapping, fine-grained filtering, low-code field and value mapping, and finally custom field filtering.

Their decisions are constrained by the choices provided in the initial domain mappings.
Currently, the low-code UI offers limited insight into the mappings and their reasons, and in some cases, mismatches arise when something that worked in chef-cli doesn't offer the right options to the user, or not all fields that should be resolved are solved.
To assist debugging such cases, chef-cli provides a command to extract the description of the low-code decisions that are asked in the UI.
Please provide this to us when reporting an issue with how the end-user mapping UI behaves.

```
chef-cli low-code --env prod > low_code.json
```

Last updated on

[Metadata extraction

Previous Page](/airsync/metadata-extraction)[Data extraction

Next Page](/airsync/data-extraction)

## Source
- DevRev developer docs: [Initial domain mapping](https://developer.devrev.ai/airsync/initial-domain-mapping)
