# Flow's Core-Protocol Working Group

The **Core Protocol Working Group** [**CP-WG**] is an open-for-all forum with
a focus on Flow's future-proof architecture: efficiently scaling without compromising decentralization and composability

## Objective
In the CP-WG, we will align on priorities of planned features, define desired features,
and iterate on the vision and roadmap for the development of Flow's underlying protocol.
A central objective is to facilitate alignment and cooperation of protocol contributors,
and to be an entry point for anyone wanting to familiarize themselves
with the inner working of Flow's protocol and its evolution.

We recommend the following documents outlining the long-term vision for Flow’s evolution:

- [Flow Core-Protocol Vision](https://flow.com/core-protocol-vision)
- [Data Availability Vision](https://flow.com/data-availability-vision)

## Scope
Evolution of Flow to the mature protocol. This includes:
* Byzantine Fault Tolerance (autonomously detecting, handling and suppressing adversarial behaviour)
* Permissionless participation
* Protocol security and cryptography
* Zero-downtime protocol upgrades
* Trustless and open access to chain data
* Massive scaling while maintaining decentralization and smart contract composability

## Organizational Details

CP-WG is part of a larger family of Working groups
[Wallet Working Group](../wallet_working_group),
[User Experience Working Group](../user_experience_working_group),
[Cadence Language Design Working Group](../cadence_language_design_working_group),
[Defi Working Group](../defi_working_group), and
[Governance Working Group](../governance_working_group).
For various topics, expertise from two (or maybe more) working groups might be needed.

We use the [meetings](./meetings) folder,
to record our ongoing meetings. For each meeting, there is
one markdown file in the format `<yyyy-mm-dd>_cp-wp_meeting<optional_details>.md`.


### Sub-Working-Groups

Depending on the scope, we plan for sub-groups to focus on specific topics:

- State Scalability
- Data Availability
- Byzantine Fault Tolerance [BFT]


### Roadmap

For the near(er) future, we anticipate that the following research-and-development areas will be an important focus for the CP-WG.


#### Dynamic Protocol State as a foundation for threat response capabilities, e.g. ban slashed node, revoke compromised keys, software upgrades

This work is a necessary premise for the Flow network to autonomously defend itself against
malicious nodes within the network. On a technical level, the Dynamic Protocol State is the foundation for
countermeasures such as slashing misbehaving nodes or entirely revoking their authorization to participate.
In a nutshell, the Dynamic Protocol State allows for updating various protocol parameters,
such as permissions to participate, during the live operations of the Flow network.

* Status: implementation completed (:point_right: [code on GitHub](https://github.com/onflow/flow-go/tree/feature/dynamic-protocol-state))
* Release date: Crescendo Upgrade
* Further reading: [Dynamic Protocol State as building block for Byzantine Fault Tolerance [BFT] and an autonomously-operating Flow-network](https://forum.flow.com/t/dynamic-protocol-state-as-building-block-for-byzantine-fault-tolerance-bft-and-an-autonomously-operating-flow-network/4906)

#### Permissionless participation of Consensus Nodes and resulting BFT requirements
While [Access Nodes can anonymously stake and participate](https://developers.flow.com/networks/staking),
Flow is currently only *partially* autonomous in its ability to handle byzantine staked nodes of other roles.
For example, a governance board (humans) evaluates the “trustworthyness” of the node operators.
Furthermore, should the node software detect suspicious actions from other nodes, it might require human experts
to look at the evidence the node collected and the governance board making a decision about punishing the offending node.

The CP-WG will contribute to the next phase in expanding support for permissionless participation to Consensus Nodes.
For example, we will be discussing engineering tradeoffs between being able to
permit some anonymous (potentially byzantine) consensus nodes earlier vs implementing an attack mitigation
as prescribed by the mature protocol or some temporary shortcut (different balances of throw-away work benefiting short-term progress,
risks to the network, technical debt and short term vs long-term development speed).

* Status: not started
* Release date: beyond 12 months
* Further reading: [BFT Master Plan](https://www.notion.so/BFT-Master-Plan-5861e287c460493d8278731f8d9f5e03?pvs=21)
  (list of engineering deliverables to achieve full permissionless participation of all node roles, not self-contained)

#### Networking-layer mitigations of message routing, DDoS, integrity attacks
Flow’s multi-node, pipelined architecture is the foundation for its unmatched scalability and efficiency.
At the same time, having specialized node roles also means that there is a highly diverse set of messages exchanged at runtime.
Established networking libraries for blockchains – like [libP2P, which Flow uses](https://github.com/libp2p/go-libp2p) – are not
equipped to protect the higher-level application logic from spamming attacks or to rank a peer's reliability across multiple
communication topics heuristically based on the traffic received from them.

As part of network layer hardening, we encompass the defense and mitigation strategies described in [this research paper](https://arxiv.org/pdf/2007.02754.pdf)
and a unified interface to rank peers holistically. At completion, a node will independently score its peers based on their
reliability and protocol-compliant behavior. Nodes will autonomously limit and reduce resources available to peers overusing libP2P control messages,
sending repetitive requests or broadcasts, or sharing messages that the protocol layer classifies as invalid or malicious.
As a result, the honest supermajority becomes resilient against a byzantine minority trying to consume network resources exploitatively.

* Status: Advanced stage of development.

  Currently, Flow can tolerate coordinated attacks of 5 malicious nodes, which will increase to 12 within the next few months.
  For non-colluding malicious nodes, the networking layer can withstand attacks of a significantly higher number already.
  Furthermore, we have detailed logic in place for node operators to blacklist other nodes as a manual fallback mechanism to
  defend against attacks that are not yet automatically handled. Later this year, Flow will be able to withstand attacks (colluding and non-colluding)
  of up to ⅓ of all nodes, which is the theoretical maximum for consensus under partially-synchronous networking conditions.
* Target completion date: Late 2024


#### Path to Zero-downtime protocol upgrades

In 2023, Flow had an uptime of 99.95%. In 2024, we want to further reduce the number of sporks for uninterrupted network availability.
During earlier stages, the ability to take down the network for a software upgrade has greatly helped the development
speed of Flow. Though, as the Flow network matures, we need more sophisticated tools to deploy software upgrades to a running network
while maintaining network availability.

At the moment, the Flow network already has Height-Coordinated Updates [HCU] as a tool to deploy protocol upgrades to the running network.
The important benefit of an HCU over a spork is that there is no downtime.
Instead, at a protocol-determined height, the nodes of a specific role just reboot with a new software image and continue,
while all other node roles remain available. Nevertheless, there are some notable disadvantages to HCUs in their current form:

1. At the moment, HCUs are only supported for Execution Nodes.
2. Time-sensitive coordination is necessary for node operators to make sure their node loads the correct image after the HCU but not too early
   in case of an unforeseen crash. As software upgrades always entail some non-zero risk, all node operators need to be on standby during the HCU.
3. When all Execution Nodes reboot synchronously, transaction processing stalls for a few minutes. Nevertheless, during Execution Nodes’ HCU,
   the Flow network continues to ingest and order transaction for subsequent execution.
   Execution nodes catch up once they are back online with the new software version.

The goal of this work is (i) to extend and refine the HCU mechanism to allow updates to other node roles (i.e. remove limitation 1)
and (ii) evaluate potential avenues for rolling upgrades that do not require nodes of one role to reboot in a time-coordinated manner
(remove limitation 2 and 3 for some upgrades).

* Status: not started
* Release date: unknown
* Further reading: tbd

#### Trustless and open access to chain data

Enabling local script execution and archival support on Access and Observer Nodes are next
milestones on the development roadmap. In the longer term, Data Availability sub-working group  
focuses on scaling the Access layer to support a terabyte-sized execution state (single snapshot without history)
up to petabyte scale at maturity.

* Further reading: [Future of Access Nodes](https://www.notion.so/dapperlabs/Future-of-Access-Nodes-9b1cc324eb5b40788a08a9404ae4505a?pvs=4)

#### Recovering from Epoch-Fallback Mode without requiring a Spork

Flow is organized in Epochs of 1 week each. Nodes can join and leave the network at epoch boundaries,
as described [here](https://www.notion.so/Epoch-Preparation-Protocol-adf8187eeced4d2dbb8a21d9fd703d5d?pvs=21).
However, before they can take over the nodes for the upcoming epoch engage in a collaborative protocol called Epoch Setup Phase.
For example, during the Epoch Setup Phase, the consensus nodes run a distributed key generation [DKG] algorithm
that sets up [Flow’s random beacon for secure random number generation](https://forum.flow.com/t/secure-random-number-generator-for-flow-s-smart-contracts/5110).
Unfortunately, the Epoch Setup Phase might fail for different reasons, in which case the new set of nodes cannot take over.

Currently, Flow has the [Epoch Fallback Mode](https://www.notion.so/Epoch-Fallback-Mode-EFM-9878522a84ec4fa6935d94f4e11ff855?pvs=21) [EFM]
as a disaster-prevention mechanism that engages to prevent a total network halt in case the Epoch Setup fails.
Unfortunately, a spork is required sooner or later after EFM engages, which in turn increases network downtime.
Goal of this work is to re-design the EFM such that recovery is possible without a spork via a governance transactions (supported by human coordination).

* Status: very early research stage.
* Release date: unknown
* Further reading: [Epochs](https://www.notion.so/Epochs-412af292863e4d8f95bf2fcd14e36612?pvs=21)

#### Scaling the State to Terabytes (single snapshot)

All data that is updated through an execution of a Cadence smart contract is called ‘Execution data’ and
is stored in a [Memory-trie](https://github.com/onflow/flow-go/tree/master/ledger) (MTrie) data structure.
MTrie serves 2 purposes - it holds all execution state data and also calculates a new hash every time the data changes.
This hash is used by verification nodes to validate the execution result.
As an tentative solution during the early stages of Flow, we chose to keep the whole state in memory, which is both simple and performant.
Though, we knew this would need to change for Flow at its mature scale with Petabytes of state size.

There are 3 technical initiatives

1. `Atree` register inlining, which optimizes the way that Execution Nodes store cadence resources in the state.
    * Status: engineering close to completion ([Atree](https://github.com/onflow/atree) on github).
    * Release date: Crescendo Upgrade (to be confirmed)
    * Further Reading: [Scaling Execution Node](https://forum.flow.com/t/scaling-execution-node/5039)

2. The `Storehouse` aims to separate the state’s registers from the trie. For transaction execution, we will solely work on a key value store that
   is optimized for low latency of reading and writing individual registers. After the execution completed, a large batch of resulting register updates
   will go to the trie, which generates the respective state proofs for the Verification Nodes. This will drastically increase the state that an
   execution node can hold for the purpose of executing transactions.

   At this stage, the trie will still live in memory. Hence, the size of the state that the Execution Node can generate proofs for is still limited by the available machines’ RAM.
    * Status: early proof-of-principle
    * Release date: unknown
    * Further Reading: [Separation of Payload store from Trie](https://www.notion.so/Separation-of-Payload-store-from-Trie-44d1cb50690448ad83b062935531f6bf?pvs=21)
      and [Scaling Execution Node](https://forum.flow.com/t/scaling-execution-node/5039)

3. The goal of the `New Trie` is to remove the remaining bottleneck of the execution state trie living in memory of a single machine.
   We target a design that can be scaled horizontally across multiple machines as well as completely offloaded to a database.
   As this requires a complete re-design of our trie anyway, we plan to include additional improvements during the redesign
   (most importantly adopting a binary radix trie supporting variable key length).
   This new trie will be the one puzzle piece for supporting completely trustless light client in the future,
   which can run on smartphones and embedded hardware.

    * Status: not started
    * Release date: unknown
    * Further Reading: [Separation of Payload store from Trie](https://www.notion.so/Separation-of-Payload-store-from-Trie-44d1cb50690448ad83b062935531f6bf?pvs=21)
* Concurrent Transaction Execution and initiatives 1-3 here have an important dependency. It should be noted that Concurrent Transaction Execution is covered
  by the Cadence working group. Nevertheless, storage scaling critically depends on the ability to concurrently execute transaction. Thereby we can compensate
  for the increased latency when the state moves from completely in-memory to a hybrid structure with some rarely accessed registers offloaded to disk.


The CP-WG is not limited to the aforementioned topics.
We invite all CP-WG participants to bring up other areas in the core protocol that they feel are important for the broader evolution of Flow.
