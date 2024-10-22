# Core-Protocol Sub-Working-Group Meeting on Versioning, May 23, 2024

**Attendees**

Alex Hentschel,
Bastian Müller
Jordan Schalm,
Leo Zhang,
Peter Argue

## Agenda

We are slowly at the point, where we have the technical capabilities (Dynamic Protocol State) as well as the ecosystem need to:
protocol versions for different parts of the protocol
software specifies which protocol versions it implements
built-in check in software ensuring compatibility

We want focus on the example of the Access Node, which should ensure compatibility of its 'execution subsystem' (Cadence+FVM+???) with the respective block for script execution.

**Goal** of this meeting

Bring together a small but representative group of flow engineers across the protocol. Align on versioning convention for 'execution subsystem'.
* version format: [suggestions] integer version or semantic (major-minor)
* software vs protocol vs smart contracts
* What change specifically compared to current version beacon desired?


_Any convention will probably be easy to change._


### Further Reading
- [Protocol Version Upgrade Mechanisms Discussion](https://forum.flow.com/t/protocol-version-upgrade-mechanisms-discussion/5717) (forum post by Jordan)

Misc links of prior discussions and related
- [[Brainstorming] HCU-style upgrades for all node roles](https://flowfoundation.notion.site/Brainstorming-HCU-style-upgrades-for-all-node-roles-b6b0ab084075432782cd0407b73479c7) (notion)
- [issue #5324](https://github.com/onflow/flow-go/issues/5324): to make a FLIP for software ↔ protocol


---
- [Video Recoding](https://drive.google.com/file/d/1f3tUqVaA425iFS8u-ldyZRHNr4u5udDx/view?usp=sharing)
- Meeting Transcript: [2024-05-23_Versioning_sub-working-group_transcript.md](./2024-05-23_Versioning_sub-working-group_transcript.md)

## Meeting Notes

### Versioning

- Execution state machine
    - including system transactions
- have technical means to force nodes to upgrade (or not participate)

### downwards-compatibility

- versioning “protocol version” by integer

  (mindset: multiple implementations of protocol, they can have different software versions/built versions, but should specify which Protocol Version(s) they support)

- Protocol Version:
    - guarantee: all implementations that support this protocol version produce the *same* result

Example: security fix for execution

- bump `Execution Protocol Version` by 1

### Idea A:

hierarchical versioning approach
```
                                                 / execution version
<Spork level integer> <protocol level version>  - verification version
                                                 \ consensus version
```

**Sub-sytems that we want to definitely version:**

- Protocol State
- Execution

and both are broadly relevant for more than one node

### Idea B:

- node starts up. It internally knows which “Protocol Version” the software speaks/supports
- if we have individual version numbers for different sub-components, we have a lot of flexibility
- versioning is largely a “key-value pairs”:
    - for “consensus” I need to support x
    - for “execution” I need to support y

### Additional considerations

- data also determines how a node behaves. Forgot a data migration, will produce wrong results.
    - we should maybe in the long run version the data
- also need the discipline to bump “supported version” in the software in our PRs
