---
title: Snap-in Platform
type: developer-doc
status: stable
source: developer.devrev.ai
category: snapin-development
source_url: https://developer.devrev.ai/snapin-development/concepts
last_updated: 2026-05-11
summary: "A snap-in platform manages snap-in packages and installs snap-ins."
---

# Snap-in Platform

Snap-in Platform

## [Snap-in platform](#snap-in-platform)

A snap-in platform manages snap-in packages and installs snap-ins. It enables snap-ins to register, validate, and deploy functions, creating other DevRev objects, registering events/webhooks, and triggering actions enriched by context.

## [Snap-in](#snap-in)

Snap-ins are collections of objects that extend DevRev's core platform value. These objects include automation, event sources, keyrings, custom types, vistas. With snap-ins, developers can develop at "arms-length" and without making any changes to DevRev's core platform.

Snap-in developers interact with DevRev objects through APIs, get updates on DevRev objects through webhooks, and register an event source to subscribe to GitHub/Slack/any external events.

## [Snap-in package](#snap-in-package)

A snap-in package is a collection of DevRev objects and their relationships that describe the functionality of the developed snap-in. It doesn't reference an object within the installer's dev org. It's a parent object collecting snap-in package versions.

## [Snap-in version](#snap-in-version)

A snap-in version is the definition of a snap-in. It doesn't belong to any dev org. It's equivalent to a snap-in source code. When a snap-in version is installed, it requires certain inputs from the installer, such as a PAT for GitHub, registering a URL on Bitbucket or some configuration.

The snap-in developer can specify some input configurations that the installer can use to customize the snap-in.

## [Automation](#automation)

In automation, the event source is linked to a function, so whenever an event occurs on that event source, the function is triggered and the event payload is passed along. All keyrings configured by the installer are included in the payload passed to the functions, along with developer-level tokens.

## [Connection](#connection)

A connection uses a keyring object to provide authentication, access token refreshment, and secret storage (access token, refresh token, PAT, API key and more). Upon creating the connection, the platform automatically refreshes the OAuth access token whenever necessary. Objects can reference secrets to access external or DevRev-protected APIs. The platform may use a connection to automatically register the webhook URL with an external source. Automations may also use connections to pass secret values to corresponding functions.

## [Event source](#event-source)

[Event sources](/snapin-development/references/event-sources) collect events from webhooks, emails, and timer-based API calls. Events can also be manually published. DevRev supports the ingestion of webhooks from any source. Each event source is assigned to a dev org.

For example, if you want to collect webhook events from an organization's GitHub, create an event source which in turn gives us a URL to subscribe to on GitHub. Webhook events published to this URL are available from this event source.

## [Function](#function)

The framework for executing code provided by users is [functions](/snapin-development/references/functions). Currently, Javascript/TypeScript can be taken as input from the user and deployed as a function.

Connection values can be passed to a function at runtime, enabling it to execute API calls to DevRev and to external systems such as GitHub, Slack, Bitbucket, and Discord.

## [Keyring](#keyring)

A [keyring](https://developer.devrev.ai/snapin-development/references/keyrings/keyring-intro) is a collection of authentication information for external systems. This includes the key (such as a PAT or an API key), its type, the organization ID for which a key is valid,
and in some cases the organization name. A keyring is used by a snap-ins to authenticate to the external system in API calls.

## [Imports](#imports)

Snap-ins that provide an extractor function for an [AirSync](/airsync) snap-in responsible for extracting data from an external system need to have an import section defined in their manifest to register their snap-in in the **Imports** section of the DevRev app.

## [Globals](#globals)

Snap-ins can be configured to enable and disable features, based on custom inputs defined by the developer and provided by the installer.

## [Commands](#commands)

A user can trigger [commands](/snapin-development/references/commands) on different surfaces based on some parameters. Once a command is executed, a function is triggered.

A developer can develop commands to be included in a snap-in Version along with associated functions. These commands are installed when the snap-in is installed.

As part of the snap-in, commands have access to keyrings, global variables, and event sources.

## [Hooks](#hooks)

[Hooks](/snapin-development/references/hooks) enable developers to invoke functions when various events in the lifecycle of a snap-in occur. Hooks can be used to perform various actions based on the event such as validating the snap-in inputs and keyrings when the configuration is updated, registering event-sources and webhooks in external platforms when snap-in is activated, or setting custom fields to be used by the snap-in.

Detailed documentation on hooks can be found in the [hooks reference](/snapin-development/references/hooks).

## [States](#states)

The snap-in can have the following states:

* *DRAFT*: The snap-in installation is in progress and the event-sources, automations, and commands aren't created yet.
* *ACTIVATING*: The snap-in is being activated, and the automations, commands, and snap-kit actions are paused. The snap-in can't be updated in this state.
* *ACTIVE*: The snap-in is functioning, and the automations, commands, and snap-kit actions can be invoked.
* *ERROR*: The snap-in isn't functioning, and the automations, commands, and snap-kit actions are paused. This state can be reached in case of any misconfiguration of the snap-in (such as invalid keyrings or inputs) or failure to activate the snap-in.
* *DEACTIVATING*: The snap-in is being deactivated, and the automations, commands, and snap-kit actions are paused. The snap-in can't be updated in this state.
* *INACTIVE*: The snap-in is paused by the user, and the automations, commands, and snap-kit actions are paused.

*ACTIVATING* and *DEACTIVATING* are transitory states and background processes and hooks move the snap-in from these states to a stable state.

The following diagram illustrates the transitions between different states.
![snap-in-lifecycle](/_next/image?url=%2F_next%2Fstatic%2Fmedia%2Fsnap-inlifecycle.fef08292.jpeg&w=3840&q=75&dpl=dpl_7YrfNpbg1U18B9yV3zCtUk5bPEKN)

## [Snap-kit](#snap-kit)

[Snap-kit](/snapin-development/references/snapkit) defines UI customization components. It's defined in the snap-in package and used to display developer-defined components. A snap-kit component can display data to a user or collect input for triggering a function.

## [Marketplace](#marketplace)

The [marketplace](https://marketplace.devrev.ai/marketplace) is a portal where DevRev and external developers can publish snap-ins and other extensions.

Similarly, developers can use private marketplaces to publish their own custom snap-ins that are scoped to their dev org.

## [Personas](#personas)

### [Publisher](#publisher)

The developer's dev org is responsible for publishing the snap-in to the marketplace. The publisher is responsible for supporting snap-in users.

### [Installer](#installer)

Installers install the snap-in, provide configuration inputs, set up the necessary keyrings, and configure webhooks for external apps.

Last updated on

[Push notifications for mobile

Previous Page](/sdks/push-notifications)[Overview

Next Page](/snapin-development/tutorials/overview)

## Source
- DevRev developer docs: [Snap-in Platform](https://developer.devrev.ai/snapin-development/concepts)
