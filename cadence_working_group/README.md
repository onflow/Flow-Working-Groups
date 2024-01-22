# Cadence Working Group

## Intro
Cadence Working Group is an open-for-all forum with a focus on Flow's Smart Contract programming language (Cadence) and it’s execution environment.

### Objectives
* Build the best programming language for developers to safely and efficiently explore new applications of smart contracts and on-chain logic.
* Represent and promote Cadence in a wider software development and Web3 community.

### History
Cadence Working Group started as "Cadence Language Design Meetings" (LDM) - series of meetings forusing on the implementation of Cadence programming language that started in Juy 2022. You can access all notes from those meetings in the ["meetings" directory in the Cadence Repository](https://github.com/onflow/cadence/tree/master/meetings).
Early 2024 this purpose of the working group was expanded to also cover topics related to Cadence runtime enviroment, a component of Flow Execution Node.

* [Current Priorities](#current-priorities)
* [Roadmap](#roadmap)
* [Meetings](#meetings)
* [Minutes/Recordings](#minutes)

### Current Priorities

- Complete & Launch Cadence 1.0 Release.

## Roadmap

| Features / Milestones | Status | Release Target | Progress | Comments |
| [Complete Cadence 1.0 Implementation](https://github.com/onflow/cadence/issues/2642) | In Progress | 30 March 2024 | On Track |All Must-have Features and breaking changes have been completed. Remianing scope covers mainly bugs and small improvements.|
| Complete [EVM on Flow Implementation](https://github.com/onflow/flow-go/issues/5241) | In Progress | Feb 2024 |  | |
| Complete [EVM JSON RPC Endpoint Implementation](https://github.com/onflow/flow-evm-gateway/issues/12) | In Progress | Feb 2024 | | |
| Complete Cadence 1.0 State Migrations Implementation | In Progress | End of Jan 2024 | | |
| Launch Cadence 1.0 and Flow EVM on [Crescendo Stable TestNet](https://forum.flow.com/t/update-on-cadence-1-0-upgrade-plan/5597) | In Progress | Feb 2024 | | |
| Launch Cadence 1.0 on [Crescendo Migration TestNet](https://forum.flow.com/t/update-on-cadence-1-0-upgrade-plan/5597) | Not Started | Feb 2024 | | |
| Start work on Cadence language specification | Not Started | | |This goal will have multiple phases, moving from informal to formal specification definition and will span range of short and long-term priorities.
It delivers incremental benefits as it progresses, in 2 core areas; efficiency of implementing new features and hardening the implementation. More specifically, it will enable efficient validation of the Cadence codebase against the specification and enforce more structured audit of the implementation as the specification is written. It will also make it more efficient to write defensive checks (e.g. resource duplication) and alternative components like compiler. In other words - instead of relying on deriving the correct behaviour from the current implementation, we will be able to derive it from specification, which is much easier.|
|Design & develop capabilities for backward-compatible language evolution and non-breaking language extensions (e.g. Cadence compilation and runtime bytecode execution in the Cadence VM).| On Hold | | | |

## Meetings

The Cadence working group breakout sessions are always scheduled in [Flow Webinars & Events calendar](https://calendar.google.com/calendar/u/0?cid=Y180Nzk3OGY1Y2Q5ZGE2MzZjYWRjNmI4NDczMTAyYjUwOTJjMWE4NjVkZDAxMDU1ODM5M2VjYjdmOWZkMGM5YWQwQGdyb3VwLmNhbGVuZGFyLmdvb2dsZS5jb20) and announced on [flow-events Discord channel](https://discord.com/channels/613813861610684416/1050190147100102787).
The breakout sessions are typically happeing on-demand, based on the number of topics for discussion collected since the last meeting. 

## Minutes
Minutes & Recordings from previous meetings will be made available here in github.
