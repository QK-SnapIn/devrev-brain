---
title: Snap-in V1 manifest
type: developer-doc
status: stable
source: developer.devrev.ai
category: snapin-development
source_url: https://developer.devrev.ai/snapin-development/references/v1-manifest
last_updated: 2026-05-11
summary: "The following guide is for the version 1 of the manifest spec."
---

# Snap-in V1 manifest

References

# Snap-in V1 manifest

The following guide is for the version 1 of the manifest spec. For the latest version, refer to [Manifest](https://developer.devrev.ai/snapin-development/references/manifest).

The snap-in manifest is what the developers write to define a snap-in. The manifest has the following sections:

## [Version](#version)

The version of the manifest. The below documentation is for version 1 and should be specified in the manifest as:

```
version: 1
```

## [Connections](#connections)

Connections are specified in the manifest with the following syntax:

```
connections:
  - name: <connection name to use in the snap-in>
    description: <detail about what this connection is used for>
    display_name: <name shown to the end-user>
    types: <list specifying what all types of connections could be selected by the end user for this connection>

  - name: <connection name to use in the snap-in>
    description: <detail about what this connection is used for>
    display_name: <name shown to the end-user>
    types: <list specifying what all types of connections could be selected by the end user for this connection>
```

Example:

```
connections:
  - name: github
    description: GitHub token to be used to get PR details
    types:
      - devrev-github-pat
      - devrev-github-oauth
```

Service that stores these secrets and has the business logic to refresh tokens, when applicable. Here is the list of currently supported connection types - [Connections](https://developer.devrev.ai/snapin-development/references/keyrings/keyring-intro)

## [Developer connections](#developer-connections)

Developer connections are defined during the development by the snap-in developer. They are available across all installations and invisible to the installer.
Only snap-in secret string type is supported for developer connections.

```
developer_connections:
  - name: <connection name to use in the snap-in>
    description: <detail about what this connection is used for>
    display_name: <name shown to the developer>

  - name: <connection name to use in the snap-in>
    description: <detail about what this connection is used for>
    display_name: <name shown to the developer>
```

Example:

```
developer_connections:
  - name: mongodb
    description: Store usage statistics
    display_name: MongoDB PAT

  - name: discord
    description: Access additional discord's API
    display_name: Discord PAT
```

The developer connection can be selected while creating the snap\_in\_version. DevRev CLI detects the developer connections in the manifest and prompts for them:

```
devrev snap_in_version create-one --manifest manifest.yaml
Please provide mapping for the developer connections:
Use the arrow keys to navigate: ↓ ↑ → ←
? mongodb:
  ▸ mongodb
    discord
```

Developer connections can only be created in the UI. They are of type "snap-in Secret".

## [Event sources](#event-sources)

Event sources are specified in the manifest with the following syntax:

```
    event-sources:
      - name: <event-source name to use in the snap-in>
        description: <detail about this event-source>
        display_name: <name shown to the end-user>
        type: <enum specifying what type of the source should be created>
        setup_instructions: <optional instructions shown to the end-user>
        config:
     <an object containing config specific to the event source>

      - name: <event-source name to use in the snap-in>
        description: <detail about this event-source>
        display_name: <name shown to the end-user>
        type: <enum specifying what type of the source should be created>
```

Here is the [list of supported event sources](https://developer.devrev.ai/snapin-development/references/event-sources).

Example:

```
event-sources:
  - name: devrev-webhook
    description: Events coming from GitHub
    display_name: DevRev webhook
    type: devrev-webhook
    config:
      event_types:
        - work_created
```

## [Globals](#globals)

Globals are implemented today using per-object schemas, which is a customization term to store custom schemas in line with the object. Each global's schema maps to a FieldDescriptor.

The definition of globals looks like this:

```
globals:
  - name: <name of the global>
    description: <its description - what is it supposed to do>
    devrev_field_type: <type of the global>
    devrev_id_type: <if the field type is id, then what are the supported object types whose id this global can store>
    is_required: <is this a required input?>
    default_value: <the default value for this global>
    ui:
      display_name: <display name for the input field>
```

## [Tags](#tags)

Define a tag by passing just the name and description of the tag.

Example:

```
tags:
  - name: github.branch.name
    description: Tag storing github branch name.
```

## [Commands](#commands)

In the manifest, you need to specify the name of the command, its namespace, the surfaces where it can show up (such as comment discussions), a description that can show up on the UI, usage hints, and the function to be triggered when the command is invoked.

```
commands:
  - name: summarize
    namespace: turing
    description: Summarizes the conversation
    surfaces:
      - surface: discussions
        object_types:
          - conversation
    usage_hint: "number of tokens to generate"
    function: generate_summary
```

For commands, the `<name, namespace>` pair should be unique across the Org in which it's installed.

## [Functions](#functions)

In the manifest, all you need to tell is the name of the function, and its description, just like tags:

```
functions:
  - name: create_work
    description: Function containing logic to create a DevRev work.

  - name: post_message
    description: Function containing logic to post a message on newly created work.
```

For functions, you also need to provide the actual JS/TS code behind this function, for that, you can refer to the README in the provided template.

## [Automations](#automations)

Automation is where you would link events from the event sources to your function. The definition of automations looks like this:

```
automations:
  - name: <name of the automation>
    source: <name of the event source specified in the manifest from which the events coming in could trigger this automation>
    event_types:
      - <event from the source on which you need to run the code>
    function: <name of the function specified in the manifest which should be run>
```

For custom event sources, whatever event key you emit from your policy, the event name would be "custom:`<your event key>`".

Last updated on

[Snap-in manifest

Previous Page](/snapin-development/references/manifest)[Keyrings: Securely connecting snap-ins to external services

Next Page](/snapin-development/references/keyrings/keyring-intro)

## Source
- DevRev developer docs: [Snap-in V1 manifest](https://developer.devrev.ai/snapin-development/references/v1-manifest)
