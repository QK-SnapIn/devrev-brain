---
title: Using a snap-in to perform a DevRev action
type: developer-doc
status: stable
source: developer.devrev.ai
category: snapin-development
source_url: https://developer.devrev.ai/snapin-development/tutorials/timer-ticket-creator
last_updated: 2026-05-11
summary: "The objective is to build a snap-in that creates a new ticket every 10 minutes."
---

# Using a snap-in to perform a DevRev action

Tutorials

# Using a snap-in to perform a DevRev action

## [Introduction](#introduction)

The objective is to build a snap-in that creates a new ticket every 10 minutes.

## [Background context](#background-context)

The [Getting Started](https://developer.devrev.ai/snapin-development/tutorials/getting-started) tutorial creates a hello-world snap-in which prints a log message when a work item is created.
This tutorial makes the following changes to the snap-in:

1. Update the trigger condition to run every 10 minutes instead of work
   creation.
2. Create a ticket whenever the snap-in is triggered.

Ensure that you have at least one [part](https://support.devrev.ai/devrev/article/ART-21849) in your organization since every
ticket must be linked to a part and have an owner.

Since a DevRev ticket is created whenever the function is triggered,
DevRev APIs need to be called that allow this
functionality. Although one can directly make HTTP requests to the endpoint,
it's strongly suggested to use the
[DevRev TypeScript SDK](https://www.npmjs.com/package/@devrev/typescript-sdk)
since it provides additional types and helper methods which ease development.

### [Installation guide](#installation-guide)

* Install [DevRev CLI](https://developer.devrev.ai/snapin-development/references/cli-install)
* Install [jq](https://stedolan.github.io/jq)
* Install [DevRev SDK](https://www.npmjs.com/package/@devrev/typescript-sdk?activeTab=readme)

If you did not follow the [getting started](https://developer.devrev.ai/snapin-development/tutorials/getting-started) tutorial then follow these steps to authenticate and initialize the snap-in TypeScript template:

```
devrev profiles authenticate -o <dev-org-slug> -u <youremail@yourdomain.com>
```

```
devrev snap_in_version init
```

#### [Trigger](#trigger)

The trigger condition for the snap-in is dictated by the
[Event Sources](https://developer.devrev.ai/snapin-development/references/event-sources)
section in the manifest. The [`timer-events`](https://developer.devrev.ai/snapin-development/references/event-sources#timer-based-event-sources)
event source is suitable for the use-case, since it allows trigger of snap-ins
using [CRON expression](https://crontab.guru/).

#### [Action](#action)

The hello-world snap-in prints a log message whenever the snap-in is triggered.
Here, the snap-in should create a work-item of type ticket when triggered. To do
that, use the
[DevRev TypeScript SDK](https://www.npmjs.com/package/@devrev/typescript-sdk) to
make API calls for creating the ticket.

### [Creating the snap-in](#creating-the-snap-in)

#### [Updating the manifest](#updating-the-manifest)

Update the manifest file to reflect the objective. Update the name, the
description, and the service account's display name to better reflect the
snap-in's behavior.

manifest.yaml

```
version: "2"

name: "Timely Ticketer"
description: "Snap-in to create ticket every 10 minutes"

service_account:
    display_name: Automatic Ticket Creator Bot
```

Next, update the `event_sources` section to use the `timer-events` event source.
The `timer-events` source type takes a `config` of type `cron` or
`interval_seconds` as mentioned in the
[documentation](https://developer.devrev.ai/snapin-development/references/event-sources#timer-based-event-sources).
The `cron` config is used here.

manifest.yaml

```
event_sources:
    organization:
        - name: timer-event-source
          description: Event source that sends events every 10 minutes.
          display_name: Timer Event Source
          type: timer-events
          config:
            # CRON expression for triggering every 10 minutes.
            cron: "*/10 * * * *"
            metadata:
                event_key: ten_minute_event
```

Finally, update the `function` name to better reflect the behavior and
`automation`name to use the event type corresponding to the `timer-events` event
source.

manifest.yaml

```
functions:
    - name: ticket_creator
      description: Function to create a new ticket when triggered.

automations:
    - name: periodic_ticket_creator
      description: Automation to create a ticket every 10 minutes
      source: timer-event-source
      event_types:
        - timer.tick
      function: ticket_creator
```

After these changes, the final version of the manifest can be found
[here](https://github.com/devrev/snap-in-examples/blob/main/6-timer-ticket-creator/manifest.yaml).

### [Renaming the function](#renaming-the-function)

Next, the function name in the `src/functions` folder needs to be renamed to
'ticket\_creator' which is the one put in the manifest.

```
src/functions/on_work_created => src/functions/ticket_creator
```

These changes need to be reflected in the following files as well:

* `src/function-factory.ts`
* `src/test-runner/example.test.ts`
* `src/functions/ticket_creator/index.test.ts`

### [Event received by the snap-in function](#event-received-by-the-snap-in-function)

In the hello-world snap-in, the ID of the created work-item gets extracted from
the input event as such.

```
console.info(
  `The work ${events[0].payload.work_created.work.id} has been created.`
);
```

The schema for a event received by the snap-in is:

```
{
 payload:Record<string,any>
 context: {
    "dev_oid": string,
    "source_id":string,
    "snap_in_id": string,
    "snap_in_version_id":string,
    "service_account_id":string,
    "secrets": {
        "service_account_token": [SECRET],
        ...
    },
 },
 execution_metadata: {
    "request_id":string,
    "function_name": string,
    "event_type": string,
    "devrev_endpoint": string
 },
 input_data: {
    "global_values": Record<string,string>,
    "event_sources":Record<string,string>,
    "keyrings":Record<string,string>,
    "resources": Record<string,string>
 }
}
```

The `payload` differs by the `event_source` and the `event_type` received. There
are two fields to be concerned about in the input payload:

1. `devrev_endpoint` the endpoint of the API call.
2. `service_account_token` which is a short-lived token provisioned by each
   snap-in. This is required when making API calls to DevRev.

### [Updating the code](#updating-the-code)

Update the code in `src/functions/ticket_creator/index.ts` to reflect the
behavior.

Firstly, import the DevRev TypeScript SDK in the `index.ts` file

index.ts

```
import {client, publicSDK} from "@devrev/typescript-sdk";
```

Next, update the `run` function in the hello-world example. Since the ticket
gets created frequently, set some creation time in the title and the body. The
example uses the part as `PROD-1` and keeps the owner as `DEVU-1`. Feel free to
edit those values to actual IDs for parts and users in your dev org.

The complete `index.ts` file looks like this

```
import { client, publicSDK } from "@devrev/typescript-sdk";

export const run = async (events: any[]) => {
  for (const event of events) {
    const endpoint = event.execution_metadata.devrev_endpoint;
    const token = event.context.secrets.service_account_token;

    // Initialize the public SDK client
    const devrevSDK = client.setup({ endpoint, token });

    // Create a ticket. Name the ticket using the current date and time.
    const date = new Date();
    const ticketName = `Ticket created at ${date.toLocaleString()}`;
    const ticketBody = `This ticket was created by a snap-in at ${date.toLocaleString()}`;

    const response = await devrevSDK.worksCreate({
      title: ticketName,
      body: ticketBody,
      // The ticket is created in the PROD-1 part. Rename this to match your part.
      applies_to_part: "PROD-1",
      // The ticket is owned by the DEVU-1 user. Rename this to match the required user.
      owned_by: ["DEVU-1"],
      type: publicSDK.WorkType.Ticket,
    });

    console.log(response);
  }
};

export default run;
```

### [Deploying the snap-in to your organization](#deploying-the-snap-in-to-your-organization)

Once satisfied with the code changes, move to the `code` folder, and run

```
npm install

npm run build

npm run package
```

This builds and packages your snap-in and creates a `build.tar.gz`. The `tar.gz`
and `manifest.yaml` file is used when creating the snap-in version.

Always remember to build and package the snap-in whenever there are code changes
and it needs to be re-deployed.

Steps for deploying this snap-in have been discussed in the
[Getting Started](https://developer.devrev.ai/snapin-development/tutorials/getting-started) section.

## [Resources](#resources)

The final snap-in code and manifest can be found
[here](https://github.com/devrev/snap-in-examples/tree/main/6-timer-ticket-creator)

Last updated on

## Source
- DevRev developer docs: [Using a snap-in to perform a DevRev action](https://developer.devrev.ai/snapin-development/tutorials/timer-ticket-creator)
