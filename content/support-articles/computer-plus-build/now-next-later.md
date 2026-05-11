---
title: Now, Next, Later
devrev_id: ART-21871
parent_directory: Computer+ Build
translation_group: 7mRu6f0x
modified_date: "2026-02-11T05:58:57.235Z"
source_url: "https://support.devrev.ai/en-US/devrev/article/7mRu6f0x"
tags: []
top_category: Computer+ Build
wiki_match: features/templates
match_score: 0.435
last_updated: 2026-05-11
summary: "Traditional scrum processes have become outdated due to their rigid roles, fixed sizing estimations, universally applied sprint durations, and repetitive meetings like stand-ups and retrospectives."
---

# Now, Next, Later

## Continuous planning

Traditional scrum processes have become outdated due to their rigid roles, fixed sizing estimations, universally applied sprint durations, and repetitive [[entities/meeting|meetings]] like stand-ups and retrospectives. While sizing estimations help in allocating resources and predicting outcomes, they [[glossary/don|don]]'t address the most critical question. The accuracy of estimating the smallest elements of a plan only becomes clear when the plan transforms into action, and uncertainties are resolved or better understood. This lack of certainty often prompts developers to either overestimate when dealing with complexity or focus solely on known factors, resulting in a risk-averse approach.

Continuous planning represents a real-time relationship between what is planned and what is being worked on. This approach directly enables developers to pick up work that drives customer and business impact on a continuous basis. The power of continuous planning comes through deconstructing complex processes in favor of more intuitive and integrated [[features/workflows|workflows]].

## Prioritized work

Instead of antiquated concepts requiring domain knowledge, prioritized work is defined by a state machine into *Now*, *Next*, and *Later* ([[glossary/nnl|NNL]]).

- **Now**: A direct reflection of keystrokes, not what is planned but what is being executed. By capturing *Now* as a reflection of active development, a real-time meter can help teams understand true effort.
- **Next**: A prioritized, scoped estimate of what will be worked on in a given timeframe.
- **Later**: A combination of prioritized and new customer feedback that can be valued and ranked based on a combination of human and machine-based scoring.

As [[features/issues|issues]] are moved into *Next*, like traditional methods, the effort is estimated or broken down further such that the work can be completed in a given time interval. Instead of asking and evaluating a work item based on a "no more than" estimate, teams should ask for a "no less than" estimate. Developers find more comfort in proposing this value as it removes the negative connotations of exceeding an estimate and removes incessant requests to explain why the work isn't complete. This adjustment removes a lot of overhead and distractions that cause teams to over-index on effort estimates.

The final change in adopting a continuous planning process is creating a culture that cultivates adaptation. Adaptation isn't something that can be taught; you have to empower an adaptive mindset and give developers the freedom to experiment and iterate to the right solution. As auto-ranking helps prioritize future investment, small experiments help prove or invalidate hypotheses, enabling teams to continuously iterate and validate assumptions. Empowering creators to embrace adaptation enables them to maintain product- and customer-centricity when building and iterating toward a goal.

## NNL vista of issues

- **Now**: Issues that are in progress (In Development, In Testing, In Review, In Deployment)
- **Next**: Issues that will be taken up next (Prioritized)
- **Later**: Issues that are not prioritized yet (Backlog)

You can view issues according to their stage in the DevRev app under **[Work > Now, Next, Later](https://app.devrev.ai/?vista=vista-def-now-next-later)**.

![Now, Next, Later](don:core:dvrv-us-1:devo/0:artifact/4100171)

You can export views to CSV or JSON by selecting **Actions** in the upper-right corner and choosing the format.

Sprints are automatically designated as two weeks long. You can change the sprint duration by clicking the date range in the **Now** selector and changing the value of **Duration**.

![Stage duration](don:core:dvrv-us-1:devo/0:artifact/4100175)

Admins can save the duration change to make it effective for the org.

## Source
- DevRev support [[entities/article|article]] [Now, Next, Later](https://support.devrev.ai/en-US/devrev/article/7mRu6f0x) (ART-21871)
