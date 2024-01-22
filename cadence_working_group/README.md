# Cadence Working Group

## Intro
Cadence Working Group is an open-for-all forum with a focus on Flow's Smart Contract programming language ([Cadence](https://cadence-lang.org/)) and it’s execution environment.

### Objectives
* Build the best programming language for developers to safely and efficiently explore new applications of smart contracts and on-chain logic.
* Represent and promote Cadence in a wider software development and Web3 community.

### History
Cadence Working Group started as "Cadence Language Design Meetings" (LDM) - series of meetings focusing on the implementation of Cadence programming language that started in July 2022. You can access all notes from those meetings in the ["meetings" directory in the Cadence Repository](https://github.com/onflow/cadence/tree/master/meetings).
In the Early 2024 the purpose of the working group was expanded to also cover topics related to Cadence runtime enviroment, a component of Flow Execution Node.

* [Current Priorities](#current-priorities)
* [Roadmap](#roadmap)
* [How To Engage With The Cadence Working Group](#How-To-Engage-With-The-Cadence-Working-Group)
* [Minutes/Recordings](#minutes)

### Current Priorities

- Complete & Launch Cadence 1.0 Release (Covered by milestones 1-6 in the roadmap table below).

## Roadmap

| Features / Milestones | Status | Release Target | Progress | Comments |
| ---------------------------------------------------| --------- | -------------- | --------------- | ------------- |
| 1: [Complete Cadence 1.0 Implementation](https://github.com/onflow/cadence/issues/2642) | In Progress | 30 March 2024 | On Track |All Must-have Features and breaking changes have been completed. Remaining scope covers mainly bugs and small improvements. [Learn more about Cadence 1.0 changes](https://forum.flow.com/t/update-on-cadence-1-0/5197).|
| 2: Complete [EVM on Flow Implementation](https://github.com/onflow/flow-go/issues/5241) | In Progress | Feb 2024 |  | |
| 3: Complete [EVM JSON RPC Endpoint Implementation](https://github.com/onflow/flow-evm-gateway/issues/12) | In Progress | Feb 2024 | | |
| 4: Complete Cadence 1.0 State Migrations Implementation | In Progress | End of Jan 2024 | | |
| 5: Launch Cadence 1.0 and Flow EVM on [Crescendo Stable TestNet](https://forum.flow.com/t/update-on-cadence-1-0-upgrade-plan/5597) | In Progress | Feb 2024 | |Learn more about the launch plan [here](https://forum.flow.com/t/cadence-1-0-upgrade-plan/5477) |
| 6: Launch Cadence 1.0 on [Crescendo Migration TestNet](https://forum.flow.com/t/update-on-cadence-1-0-upgrade-plan/5597) | Not Started | Feb 2024 | | Learn more about the launch plan [here](https://forum.flow.com/t/cadence-1-0-upgrade-plan/5477)|
|Design & develop capabilities for backward-compatible language evolution and non-breaking language extensions.| TBD | | | On hold until we have capacity. One area of focus is for example Cadence compilation and runtime bytecode execution in the Cadence VM.|
| Start work on Cadence language specification | Q2 2024 | | |This goal will have multiple phases, moving from informal to formal specification definition and will span range of short and long-term priorities. It delivers incremental benefits as it progresses, in 2 core areas; efficiency of implementing new features and hardening the implementation. More specifically, it will enable efficient validation of the Cadence codebase against the specification and enforce more structured audit of the implementation as the specification is written. It will also make it more efficient to write defensive checks (e.g. resource duplication) and alternative components like compiler. In other words - instead of relying on deriving the correct behaviour from the current implementation, we will be able to derive it from specification, which is much easier.|


## How To Engage With The Cadence Working Group

We will be updating The [Cadence Language Design Working Group](https://forum.flow.com/t/cadence-language-design-working-group/5437) forum topic to announce new meetings - you can subscribe to the forum post to receive email notifications by pressing the "bell" icon.
The Cadence working group breakout sessions are always scheduled in [Flow Webinars & Events calendar](https://calendar.google.com/calendar/u/0?cid=Y180Nzk3OGY1Y2Q5ZGE2MzZjYWRjNmI4NDczMTAyYjUwOTJjMWE4NjVkZDAxMDU1ODM5M2VjYjdmOWZkMGM5YWQwQGdyb3VwLmNhbGVuZGFyLmdvb2dsZS5jb20) and are alo announced on [flow-events Discord channel](https://discord.com/channels/613813861610684416/1050190147100102787).
The breakout sessions are typically happening on a monthly basis, but additional sessions might be scheduled on-demand (as often as twice a week), based on the amount and urgency of topics scheduled for discussion.
Anyone can request a topic being added to the meeting agenda by contacting the [Cadence-builders Discord channel](https://discord.com/channels/613813861610684416/1108479699732152503).

## Minutes
Minutes & Recordings from previous meetings will be made available here in github.
