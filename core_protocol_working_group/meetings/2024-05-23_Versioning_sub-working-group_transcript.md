# Core-Protocol Sub-Working-Group Meeting on Versioning, May 23, 2024 - Transcript

**Attendees**

Alex Hentschel,
Bastian Müller
Jordan Schalm,
Leo Zhang,
Peter Argue


## Transcript

**Alex Hentschel**:
Hi, everyone. This meeting is an attempt to move something forward internally where I think we, the, the, we, we only need to agree on an, a sort of MVP convention. Um, but I would like to, to move this forward if he can. And it's, um, and it's around sort of resulting out of this question of, okay, we have an access node who potentially should execute script on data from within the sport. The sport could be a year long up to, and we are probably going to have different execution nodes or sort of different execution environment versions with HEUs in between. And how do we track that and version it? I mean, that's sort of the one idea. I think that that was kind of the point, Peter, where we talked about having this meeting. And the other aspect is that With Jordan and Yuri, we have implemented the dynamic protocol state, which also sort of provides us with some primitives to track versions, but we haven't really done it yet. And I think what's most missing at the moment to sort of just start to experiment and see how it's going is an agreed upon convention of How do we version the protocol, sort of the algorithm? How do we version what of the different protocols the software supports? And how do we represent that in a clean and non-confusing way? And if everything goes well, we're going to walk out of this meeting with a convention, which we can change at any time. As I said, I don't think it will be much work. Yeah, so that's sort of the premise for the meeting.

**Alex Hentschel**:
Any thoughts on this?

**Alex Hentschel**:
Great, thank you.

**Alex Hentschel**:
Sorry, let me pull up here my meeting notes. OK, so the first thing I was thinking is maybe concretely to talk about, well, what is the execution environment? So obviously, there is cadence. There is the flow virtual machine.

**Alex Hentschel**:
Is there, what's beyond that? So if you wanted to say, okay, we're, we're going to give that one version, or maybe do we want to give it different versions or have a more sort of, you know, a cadence one version, FEM one version. Um, yeah, Jordan, go ahead.

**Jordan Schalm**:
To me, the most useful way to think about it is not in terms of which software components happen to be involved, but more in terms of, like, abstractly, you have an initial state, you add a block, you execute it, you end up with a final state plus a bunch of events. And one version will be guaranteed to give you the same output, given the same input. And maybe it involves FVM. Maybe it involves some other random software component that FVM is depending on. But the most important thing is kind of that abstract functional transition from executing a block, in my mind at least.

**Alex Hentschel**:
I agree with that. I'm not quite sure, though, at what granularity we want to assign that version. Do you know what I mean? Because in the most extreme case, we would have one version for the entire protocol. And that would mean that each time we do an HCU, you know, the execution or something changes there, the consensus nodes would also perceive that as a protocol version change, which I'm not sure is maybe that's doable, but I'm not sure that's the most practical. Does that make sense?

**Jordan Schalm**:
Yeah, yeah, no, it makes sense. I just like I think you can version only whatever we want to call it. In the forum post I made, I called it the execution state machine. I think you can version that on its own.

**Jordan Schalm**:
Without the consensus nodes needing to worry about it necessarily.

**Peter Argue**:
Yeah, I think. I think what would make sense to me was to version. Different aspects of the protocol, such that only the nodes that care about that aspect need to pay attention to the version. So the execution state machine is only cared about by execution verification and access nodes, whereas consensus is maybe all the nodes need to care about that.

**Peter Argue**:
And they could be independently versioned in a way that nodes could have, they don't necessarily have together.

**Peter Argue**:
I think another piece of the puzzle, I think there's probably some smart contracts that are involved in the execution state as well, or execution state machine. For instance, the transactions that are used to execute the system transaction should be lumped in. I imagine there's some system I'm not super familiar with all of the protocol level smart contracts, but I imagine there's some in there that if they changed, they would change the execution. But maybe they're all on chain. I'm not totally sure about that.

**Peter Argue**:
I'm thinking about some of the embedded scripts that we use. I know they're used for various things on execution nodes. But maybe that's kind of lumped into the FDM.

**Bastian Mueller**:
you Yeah, my question would be, I think exactly what you pointed out, Alex, that even when we have HCUs, there's the case that some nodes don't update. We've seen that very frequently where we take inventory of what versions different node operators are running, and they run drastically outdated versions, like three, four versions behind.

**Bastian Mueller**:
Is one of the goals of the versioning scheme to have this ability to run older versions? For example, if you would adopt something like Sember, then you could have a system that is newer, but it's only patched to a new level and it's compatible with an older one. Like, you know, they produce the same execution results. Still, like, the version that this one is running is, like, maybe more performant or something, right? Is that one goal? Because, like, I think what Jordan said was, like, oh, I don't care, you know, what that versioning is or even what software is part of it, as long as it's producing the same result. Like, you could, for example, have, like, a sequential number. Every time we make a change, it's just incrementing by one, but then we don't have this compatibility, right? So is that a goal or a non-goal with that burgeoning scheme?

**Alex Hentschel**:
I'll jump in and answer your first question first to just get that out of the way. So with the dynamic protocol state, we have the technical means to force nodes to upgrade or put slightly differently. The node itself will recognize if it's running an outdated version and will say, I can't participate anymore. And maybe enter a crash loop or whatever we want, however we want to expose that information to the node operator. But it's essentially a forcing function on a technical level. Which I think is great.

**Alex Hentschel**:
And that reduces the need for compatibility. But I think you have a very important point there about downwards compatibility, for instance, of optimizations. And do we want to represent that or not? I think Jordan has very good thoughts on that. He has written a blog post. But go ahead, Jordan.

**Jordan Schalm**:
want to explain that yeah in my in my mind there's like let's just call it the protocol version the execution state machine version I don't see any reason for those to be anything other than integers because Either it's compatible or it's not, right? And maybe there are many, well, there will be many software versions with different performance characteristics or that fix some bugs which map to the same protocol version or execution version. But when we're talking about making sure that everyone who produces or executes a particular block is always guaranteed to use exactly the right version, I think, I don't know. You can use semver and just compare on the major version or whatever.

**Jordan Schalm**:
Yeah, whatever kind of thing you build on top of that. But to me, it makes sense for that to be strictly integers and strictly baked in to the software and separate from however we define the software version, like the tags and so on.

**Bastian Mueller**:
Yeah, that makes a lot of sense. And then I think currently we're in the state of like, well, we have one implementation of the protocol. It's the reference implementation. It's the only implementation and it sort of defines what the protocol is. But, you know, there are other blockchains where you have multiple implementations of the same protocol. It's specified. And I think that should be sort of That protocol version should be abstract enough to define that and be not tied to the software version.

**Bastian Mueller**:
For example, just looking at execution, there are so many things that influence the execution results. Cadence version, core contracts versions, smart contracts that are part of the core protocol, crypto library, there's so many things. I don't think that it makes sense to have separate versions for them individually.

**Bastian Mueller**:
You know, I totally agree with what you sort of said at the beginning of like, as long as we have a version and it sort of always produces the same result, then that's all we sort of need. I don't know how that is possible for consensus and these other parts.

**Bastian Mueller**:
But at least from the execution part, that makes a lot of sense.

**Bastian Mueller**:
So maybe concretely, if we were to ship a security fix, what would that ideally look like, Pretty much it would change the execution results, so we would bump that version.

**Bastian Mueller**:
what version do we bump, like we would have like an execution specific version number and say like, oh, we hereby declare that all the nodes need to be compatible with execution, execution version, or, you know, like that execution protocol version, like two, one is outdated now, you need to, you need to update, and they would be incompatible if you don't update to that Execution specific version because nothing has changed about consensus, right? It's purely like a security fix for execution wherever that might be crypto or cadence or some other Software component, but definitely it changes the execution result Then then all the other nodes would be kicked off the network essentially like they have to They have to update But just thinking through that, how that would look like, which makes a lot of sense, just like spelling it out.

**Alex Hentschel**:
I like that example. And as you're talking through it, I'm like immediately wondering about two different scenarios, right? So there is the execution version, which is like, what results do we produce? And then there's sort of a very small side effect of How do execution nodes and verification nodes communicate, for instance, to consensus that they agree, you know, that they have checked a certain thing? And just because, you know, the execution node is maybe, I don't know, now throwing an error in cases it would previously allow a transaction to succeed, you know, like, I don't know, illegally copying a resource, for instance, right? So now that errors. OK, great. So execution and verification nodes and maybe access nodes have to understand that. But the sort of higher level interface between execution and consensus of, oh, I produced this result with root hash, blah, blah, blah. And verification nodes say, I'm agreeing with that. That hasn't changed. So where do we draw that line? Do we maybe also need a version for the interfaces?

**Alex Hentschel**:
That could be one interesting question. And I think it might help us here to kind of really concretely stay on the example of the access nodes, because I think that's sort of the most immediate, or at least there, you know, we want to move ahead with sort of some technical changes. And I feel like that would be a good example to just sort of talk through.

**Bastian Mueller**:
Yeah, I think there are a lot of dependencies between the different components and you probably, if you want to draw, I'm having a hard time sort of knowing much more. What's above execution sort of consensus and access nodes, like limited knowledge there. But how I understand, please correct me if I'm wrong, but like a consensus version is basically relying on execution. So if the execution number is bumped, you would kind of have to bump the consensus version too, right? Because that's sort of like a dependency from consensus on X, or is that not the case?

**Alex Hentschel**:
Well, at least there's an API, right? So if that API changes, but arguably you can, most of our changes on the execution will probably not touch that API. Like how chunk data packs look and sort of how an execution result looks. I think most changes in practice don't affect that API. So we could decouple it.

**Jordan Schalm**:
I would actually, sorry, I would like almost reframe that as saying, if you are changing models in the protocol, like an execution result, then that just is a protocol upgrade. But like Alex said, I agree, I think most execution state machine or cadence or FBM changes wouldn't necessarily do that.

**Alex Hentschel**:
So in this particular case, sorry, Batran, go ahead.

**Bastian Mueller**:
Yeah, just a follow-up question. What I'm thinking through is, you have an HCU and we're updating some part, whatever that might be. And then the end goal is figuring out for access node, do they need to be updated as well or not? And so there is like a dependency chain, right? All the way, like access depends kind of like, I think on consensus and on execution. And so there are these dependencies and I don't really see how.

**Bastian Mueller**:
And again, it's like lack of knowledge, but like, isn't it kind of the case that if you have two consensus nodes. And they are part of the network and they're currently running. And then an execution node is like a couple execution nodes are running and we say like, okay, let's deploy an execution protocol version bump. The execution nodes get updated. They need to be updated to this new version too. They're now compatible. Does it somehow affect consensus and access node at all? No, they don't care about details like what results are produced. They still produce the same data structures and protocol things. So it doesn't really matter for them. So for example, one change that is part of execution, but isn't like a Patents is for example, like crypto, like, Oh, the crypto library is like producing a different cash now or something. So that influences the execution results, bug fix, whatever. Does that matter to consensus or it doesn't care at all? Like, like maybe it's good to like have a diagram and, and, and draw lines, like sort of, I'm a visual person person, but like sort of knowing what the dependencies are and then drawing boundaries of like, what's sort of independent. I don't know.

**Leo Zhang**:
Yeah, I'm hearing all the ideas and the requirements. And I thought of maybe a solution. I'm just throwing this out to hear some feedback. So I also run into this case a lot. For example, I need to fix some execution node changes. But this is execution node changes only. And it also does not require an HCU.

**Leo Zhang**:
bump a version still. But I would only build an image for execution node. So as if I'm only building an upgraded version for execution node. But when there is an execution node upgrade, which requires an HCU, we also make a new version of the execution node, an execution node, but not other nodes, bump up the version. So other nodes will who have their version kind of behind, right? B0.33.2, and where execution node is already 0.33, maybe something within HCU. So, but you could, in the future, if we have one year of, without a spork, we might upgrade consensus node and other nodes without an execution node, right? Or we might upgrade all the nodes altogether. So which means sometimes we have at least three types of upgrades. One is very minor upgrade optimization, or a specific node only. I'm just fixing a certain API issue or deploy a new feature to, for example, one type of the node, like execution node.

**Leo Zhang**:
So we built an HCU. This is the first type of upgrade. Second type is to execute the node. You want to deploy, you want to bundle a bunch of upgrades, including cadence upgrades, smart contract upgrades, crypto upgrades, all together with an HCU. And that requires an execution node HCU and upgrading execution node and verification node. And we want to indicate that if we bump this version, then all the nodes that are different from this version would not be compatible with this. And you have to bump your version to be aligned with this version. And this is the second type of And if you have the first type of upgrade, as long as you don't have the second type of upgrade, then you're still compatible. And the third is... Is maybe the protocol level upgrade, like all the nodes need to upgrade in order to be compatible. For example, if we want to change the network, the P2P interface, how nodes can communicate with each other, it would be maybe a broader upgrade, and you won't be able to talk to other nodes without an upgrade. So one idea to accommodate all these three types of upgrades is maybe let's say we have a digit for each node type and we also reserve one digit in the version for like a kind of global protocol-level version. And then we have the first version as spork-level version, right? 33, usually. We use that as a spork-level version. So if it's 33, we know it's the same spork.

**Leo Zhang**:
If we bump that version, it means it's another spork. The root block is different. And then the second number after the protocol version is the kind of global all nodes level upgrade if that version is bumped then you know any version below that will be incompatible and you have to upgrade that version to be compatible with any other nodes this is to introduce maybe certain breaking changes that requires the entire protocol level hcu and after this digit then it becomes very flexible we have four different digits for each node type. Let's say we have four digits. The first digit is reserved for the execution node, a second digit is reserved for the consensus nodes, and the third is for the access nodes.

**Leo Zhang**:
Verification node, maybe I don't think that requires specific digits. Let's say we just have three types, right? One for execution, one for consensus, one for access.

**Leo Zhang**:
So if execution node has a HCU, then we bump this version from 0 to 1. If another HCU would bump this first digit from 1 to 2. So if we look at this first digit of execution node, then we know that whether your version as execution node is compatible with the network. If I'm deploying some small fixes, I'm using another digits just for very minor very minor backward compatible upgrades. So as long as the digits for the execution node and the consensus nodes are the same, then the last digits is fine. So if I look at your execution node and my execution node version, as long as the first two digits are the same, And let's say we could assume that you can upgrade between these versions and still being backward or forward compatible, basically compatible with other nodes. So it's flexible to ship changes, right? We just bump up versions. As long as it's backward compatible, we just bump the last digit versions. And if it's really protocol version, HCU type of upgrade, then we bump up the node-specific versioning. So So we have now just keep using a simple version for everything. We don't have to distinguish the software version and the protocol version. It's just a simple one version and work. As it's working right now. And the version has been used in the small contract HCU as well. A small contract HCU doesn't define what digits, whatever, it's just a string. And it's up to us how we parse this string to recognize the different versions and their meaning.

**Leo Zhang**:
it's easy to implement because we have everything working with the software version. And then we can also have this sequentially incremental versioning for different types and support HCU for different node types. Yeah, I'm just throwing my ideas here.

**Alex Hentschel**:
I have a question around this, Leo. So the way you presented that, It had sort of a hierarchy, right? The highest level is the SPARC level, then you have the protocol level, and then the third level was sort of node-specific version.

**Alex Hentschel**:
What would break in your mind if we just sort of didn't have a hierarchy, right? Let's say we had We had a protocol level version, you know, and then we had a level, level of like, let's say execution, right? Then, uh, one version for one version counter for, for consensus, you know, without any sort of hierarchy. Oh, if the things before work, then you're compatible and it's or batch. And otherwise they're not like, can, can we just have them in sort of as, as, as individual counters? Would that work in your mind?

**Leo Zhang**:
It could work and yes, so if we use the hierarchy that I described, then there are certain things that we can't do. For example, if we do a protocol level HCU, then we would also reset the execution version back to zero, which means if you are running on an old version, as if you cannot talk to each other, which is that even though there is no changes in cadence, let's say, we are just upgrading maybe libp2p and the way the nodes communicating with each other, right? We changing from gRPC to maybe HTTP or whatever, that require maybe a protocol level HCU to upgrade. However, there's no cadence change. There's no FVM change, right? So the execution result is supposed to be compatible. However, if we have this hierarchy and then you bump the protocol version from, let's say, 1 you 2, automatically reset all the other versions back to 0. But if you say, OK, the protocol level is also independent with the execution version, then yes, you can do what I described. That if we update local level stuff, and it's still backward compatible for other, it's making the assumption, basically. I feel like if you take the version out of that hierarchy, you are assuming If you bump up that version, then the execution node without that version bumped can still be compatible with the nodes that bumped. So I'm designing a system where we do have some hierarchy. And the hierarchy is to say, if I have a version higher than you, then it assumes that the execution result will be different. Even though it's the same, then I will still not recognize it, and it forces you to upgrade. And I think this is still flexible, right? You can choose not to use that one, and you can choose to use other digits to bump up the version to describe your compatibility, basically.

**Leo Zhang**:
The reason I put this hierarchy is so that it allows us to have a way to describe a global-wise HCU and a way to say, you have to be on this new version to be able to participate in this new network. And we are not backward compatible to be able to do that. So if we don't have this hierarchy, then you don't have this way. And is it okay that if we don't have this way, it might be okay? But I feel like having this is better than not, right? Even if you have the option to not use this version at all.

**Alex Hentschel**:
All right, thanks for explaining that. Before I let others jump in here, the only aspect as a second aspect I wanted to touch on is, so you have a hierarchy and the other thing you kind of what an integral part of your proposal was that we only have one version number, you know, we're not versioning protocol from software independently. I think that is a potentially somewhat dangerous assumption because, you know, then we don't have the ability to say this software version speaks to different or supports two different protocol versions. And then we can't express that anymore. And I think that's probably a very important aspect in our update strategy to say, OK, I'm rolling out a software version. Who's to know it? The network is still on the old version, but I'm rolling that new software version out. It speaks the old and the new version. And then once the network switches its protocol version, then my software already supports that. But if you only have one software version, then I think it becomes, you know, and use that synonymously for protocol as well as sort of the software implementing the protocol, then I think it becomes very hard to express that.

**Alex Hentschel**:
Yeah, this sort of, oh, I can do both. And I was wondering what your thoughts on that are.

**Leo Zhang**:
Yeah, it's quite complex because we have so many different node types. And then we want to use a version to describe the compatibilities. And you have to set the rule to say which digits you use to describe the compatibility. As long as this digit is the same, then you are compatible.

**Leo Zhang**:
Yeah, I don't have a good idea. I don't have a good idea on this.

**Alex Hentschel**:
Okay, then maybe it would be sort of the next step would be, I think Jordan has written that up in his blog post a little bit more into detail. Yeah, all right.

**Alex Hentschel**:
Thank you.

**Alex Hentschel**:
Bastian, do you want to take over or not take over but go on?

**Bastian Mueller**:
Sorry, I'm not really up to date with the prior discussions. You keep on referring to that blog post. I haven't read it. If you could share a link, that would be great. Maybe it brings me up to date.

**Alex Hentschel**:
Yeah, it's in the invite too. I'll just drop it in here.

**Bastian Mueller**:
Usually people online. Thank you. Yeah, I like, Maybe before we talk about a very specific implement solution, I think one guiding principle is maybe, or could be, is that we want to keep this as simple as possible. It's quite complex what we are building, like a lot of different components, and the simpler the better. Especially we can maybe also make the assumption that at the moment, at least, and I think also in the foreseeable future, given that we want to build sort of an MVP, and then maybe, you know, like expand it in the future.

**Bastian Mueller**:
Like we have the case that there's only one implementation of the protocol and it is sort of the software protocol goes hand in hand that is the case and will be for the foreseeable future. So maybe that's something to leverage to keep things simple. We can maybe accommodate The possibility for other implementations, right, like half the split protocol and software versioning. But it doesn't really add too much, given that they are kind of like coupled at the moment. So that's that's one point. So I kind of like the US proposal of like maybe just having one thing. And even that one thing on its own is already or complex, right, like all these different components that are part of the version number.

**Bastian Mueller**:
Yeah, that was the only thing. It would be nice to keep it simple. I don't have a good proposal, but at least I like the idea from Leo to keep things simple.

**Jordan Schalm**:
I'm pretty strongly against coupling the software version and the protocol version. I think if whatever protocol version we decide on is simple enough, then we can maybe embed it in the software versioning as a pattern or whatever. But does I feel like right now we use the software version to define how we do HCUs. And there are a lot of problems with it. And it's quite fragile, in my opinion. And the thing that I keep coming back to is, ultimately, we need to say, at a certain point, you must be on this version. We're very strictly defining.

**Jordan Schalm**:
You're either compatible or you're not. There is no wishy-washy in between, which is what software versioning kind of largely defines with the major and minor versions.

**Jordan Schalm**:
The other thing I just wanted to point out, I like your idea, Leo.

**Jordan Schalm**:
of kind of even maybe if we don't go with that as like kind of a summary, you could say here's a software version, here's kind of a notation to summarize how it relates to whatever protocol version we have.

**Jordan Schalm**:
One thing I wanted to point out though is The two subsystems that we do, I think, definitely want to version at this point, the protocol state overall and the execution state. Both of them are not tied directly to one node role. Protocol state is all node roles and the execution state stretches across several. So I don't think that versioning based on node role kind of matches well with what we want to define.

**Unidentified Speaker**:
VICTOR-LOPEZ-SALGADO.

**Leo Zhang**:
Yeah, I understand.

**Leo Zhang**:
I just feel like keep one version is simpler. And then let's say if we don't keep one version, right? Let's assume that maybe the way that you describe, let's say, I can think of is maybe you have a file in the protocol, right? Defines the version of protocol, let's say a file called protocol.version. And you have another file called execution.version that describes the versioning. And every time we do HCU for execution node, we bump maybe the execution version, if we upgrade the protocol level stuff and we bump up that version, and then whenever you build a new image, the two version files, the versions include, it's also built into the image, right? Delivered together. And if we say this approach is close to what you described, Jordan, and then we can think of these two files being a single digit in the version number itself. Instead of currently v0.33.10, and we say v0.33.1.2.10, and 1 for the 2 protocol version, one for the execution version.

**Leo Zhang**:
And whenever you build an image, you have that version in the software version that is clearly seen. And by looking at the version without looking at the image itself into that file, we already know if the two versions will be compatible or not. That's the advantage of having a single version described as the software version. Because by looking at the image version, we know if this if the two nodes running on that version is compatible or not?

**Alex Hentschel**:
So I'll reiterate what Jordan just said with slightly different words, that we know for consensus, if we want to do upgrades, we have the strong requirement that we can roll out software that can say, I can speak protocol version N and N plus one. I do both. We need to be able to express that, otherwise the HCU mechanism we're now building or the versioning scheme we're now defining will probably not allow us to do most of the consensus upgrades we want to do. So we can do that, but then let's be clear that this will only be useful for execution nodes and probably not as much for the consensus and sort of protocol level. And if we want HCUs for the protocol level, respective all nodes, which I think is currently our mandate, then I think it is imperative for us to implement or come up with a versioning scheme where we can express this protocol, this software speaks both protocol or speaks this and this protocol version, you know, that we can express that. Otherwise, I think we're overly strongly limiting ourselves.

**Alex Hentschel**:
I don't know. I mean, for ENs, I have too little insights, you know, but I can only say that for consensus, it's most likely a strict requirement or put slightly differently. We lose a lot if we do not allow ourselves this sort of differentiation between software and protocol version.

**Bastian Mueller**:
Just to quickly chime in, like I think you said, like, oh, consensus wants to be able to ship software that's sort of Compatible with different protocol versions. By protocol versions, I mean consensus versions. Like, oh, I'm speaking this old consensus protocol, but I'm also able to speak the new one. The same thing we are currently not able to do because of the implementation architecture and complexities, but we want to get to that point in execution too, where we are able to like, oh, this execution node is both able to speak the old execution version where the conflicts are written in this old code and it can execute those and produce results for those. Put that old cadence version, but it can also speak the new protocol version, like execution version. And it can execute these new contracts and produce results for that version, right? Like we currently not able to, but I think that that would be nice to have. It's a longer term effort, probably not in the next year, but like, um, like if that is already a requirement for some of the components, I would make, make that like already now, like, uh, maybe like a minimum version. It's at least able to, I get the point that Leo is trying to make. If you look at the images and it has, it doesn't tell you anything about. Protocol version where it's able to speak, it's really, really hard to debug things. Jordan, I think that's what you meant with embedding. Maybe we should just have a registry and you assign, I don't know if you follow some other versioning schemes, but they use names. They just produce random names and it doesn't really matter the details, but at least it's a unique identifier. And I think Leo's scheme is trying to come up with a unique identifier and and it doesn't maybe matter too much like if it's embedded or externally recorded somewhere but having that coalition would be really nice but again like it's also nice to be able to somehow not just uh lock those two together like you know like a couple of them together like the software only speaks exactly this protocol nothing else like protocol version. We should maybe come up with names. I think you used execution protocol version. Protocol protocol version for the P2P. I don't know. Sorry, Peter, I think I cut you off there.

**Peter Argue**:
Please go ahead. I mean, I think that's a really good point about some way to identify which software versions are compatible with which of the protocol execution versions.

**Peter Argue**:
I think I'm in the camp of individual versions.

**Peter Argue**:
I think the way I envision this working would be that the versions are embedded in the node software itself. And when a node starts up, it has each node type with its own config knows which versions it is compatible with. And then it can compare that against the protocol state to say, okay, this is the version that I need to be running at this block. Do I have that version? And if not, I'm going to stop working. And so if we're articulating that as independent values, then I think it gives us a lot of flexibility to add new ones or to have certain values that only apply with certain configurations and different things like that. It gives us more flexibility in expanding on this than if we try to have a unified version.

**Peter Argue**:
I think, Leo, to your point, you were more talking about how do we articulate and the different versions for a specific piece of software. But I think if we look at it from the perspective of I'm a node and I'm starting, how do I know that I'm doing the right thing and I have everything I need? I think the individual versions makes that simpler to implement and clearer from the node's perspective.

**Peter Argue**:
But I guess some of that complexity gets pushed to operators to figure out which versions go with those specific numbers.

**Leo Zhang**:
Yeah, I want to mention, maybe I said it was improper. I said, if looking at the version number, I can know if these two nodes are compatible with each other. I think this statement maybe is incorrect, because this I remember there was an incident in the past where the versions are the same, but the data are different. So there are two things that determine if the two nodes can be compatible with each other. Not only the version, but also the data, right? If your data needs a migration and you didn't, even if you are on the new version, you are still not compatible, right? And do we save the data version in the data itself to indicate that this data is a specific version and we have migrated?

**Leo Zhang**:
And the data includes protocol data, on execution data, all types of data. Because the data are very important. The version only determines the software that we are running, but it will read the data. If we have, for example, the data stored on this table, and now the next version we are migrating to a different table, if the data is not compatible, then it's also not compatible. So yeah, I just want to bring this up. Regardless what versioning approach we are choosing, we need to cover this case as well.

**Jordan Schalm**:
Yeah, that's a good point. I something that just occurred to me with respect to The kind of operational load of figuring out which version you're supposed to use I agree. We should make that as easy as possible But I have a feeling that will get kind of automatically easier once we have a more robust system in place because right now you might run the wrong execution node version and nothing happens. And if you don't know any better, then you can just leave it there for weeks.

**Jordan Schalm**:
But if we implement something similar to what we currently have for the protocol state version for all these different things that we want to deal with, then it'll be a lot more obvious that you're running the long version. At least it'll be harder to make that mistake.

**Bastian Mueller**:
Yeah, I think the biggest gap that I have is sort of an overview of all these different components or dependencies. So I think that that's something really neat in any case, like whatever the solution is going to be, because I think I kind of understood your proposal, Peter, was like that you could have something like an access node. And I was like, I specify that I need, you know, execution or I'm compatible with execution version, you know, to And by the way, I speak like networking component version 3 and I don't care about consensus. I don't care. I'm just making things up by the way. It's just an example. I know nothing about this. And so what are those components, right? And I think your proposal, again, was not having a very static framework. For example, what Leo proposed with digits and a version number, and it's hard to extend, but make it more flexible. Almost like an arbitrary key value pair, like a mapping. This name, I need five, you know, this name, I need six. And then we just like compare versions and say yes or no. But I think that's the only thing that matters. It's like yes or no, it's not. And maybe you could have like a indicator for like minimum version or something or ranges as well. Like I speak two and three. I think it could be, I like the simplicity of it and how, and then maybe, yeah, I don't have a good answer.

**Bastian Mueller**:
or the operational overhead of figuring out what protocol this one image that you have at hand speaks. But I would build it from the bottom up. And let's define this protocol versioning system first, and then we can make it easy for operators to figure out how to run this stuff. Like because like we are having a hard time at the moment and it's really easy for operators to do the wrong thing that doesn't sound good.

**Alex Hentschel**:
Yeah in the interest of time we're approaching the last five minutes here.

**Alex Hentschel**:
So my observation from this conversation is that at the moment it's not quite clear sort of which at least there's not any universally supported proposal, you know, whether we have it more like sort of the key value pair sort of non-hierarchical versioning scheme or hierarchical versioning scheme, but I feel the It seems like there, at least a lot of people can get behind the key values sort of non-structured versioning scheme. And my question at Leo, as sort of the supporter of the alternative suggestion would be, Leo, would you be able to sort of go along with the unstructured versioning scheme, just as I said, as an MVP, you know, and maybe later on we learn better. Oh, if we're changing consensus version, we're always updating the protocol version. And then maybe we can, out of experience, impose this hierarchy in the second step. Would that be something that you could support?

**Unidentified Speaker**:
Yeah.

**Leo Zhang**:
Yeah, sounds good.

**Alex Hentschel**:
Cool. Thank you.

**Unidentified Speaker**:
Jordan?

**Jordan Schalm**:
Yeah, I just wanted to say, I think it's worth taking a step back, because we're talking very generally about this versioning system with potentially, it sounds like, many, many different versions.

**Jordan Schalm**:
Personally, I think it is very likely that we will have two versions for a very, very long time only. I don't think there is any imminent need to extend this beyond that. Even thinking between the protocol version and the execution version, Combining those is even tractable, I think. The only reason we would not combine them is for convenience, for the most part, to be able to upgrade one over the other. But I think the extent to which we would want to extend on that idea into multiple even smaller subcomponents is probably fairly limited, especially in the near term.

**Alex Hentschel**:
Well, okay. Um, I generally agree though. Um, I, I have strong reservations against the, Oh, we can, we, we can cook it down into one protocol version because I think that specifically the, um, the thought behind Peter's, uh, endeavor here is to say, I want an exit access note, which can support all the execution versions across the sport. Right. And for a year long sport, that's probably going to be more than one. And most likely, they're all going to speak one protocol version, and I don't have to deal with the complexity of, oh shit, I'm deserializing a header here from my database. Is that header version A or is that header version B? That's very unlikely, but I think it will be overwhelmingly likely that there will be two different execution node versions. So I think that's sort of my gut feeling, and I would actually be almost inclined to make it three versions. Because we have the protocol state, we have the execution node, and then we have all the messages that the nodes exchange, the format of those messages. If you have a new field, that's a new protocol version, period. And so maybe that's the next step for us to see at what granularity you want to start at and write down a very concrete proposal.

**Bastian Mueller**:
So were those the two things that you referred to, Jordan? Like you said, in the foreseeable future, there will be only two?

**Jordan Schalm**:
Yeah, to me, the things we mostly definitely need to version is the protocol and the execution state.

**Jordan Schalm**:
Yeah, those two things.

**Bastian Mueller**:
And what about things like networking? Like, is it encompassing with what you said, Alex, the data structures and how, you know, like how nodes speak to each other? Because I think like, you know, execution node pulls from consensus, but if the data structures are wrong or like the, you know, protocol, network protocol is different, then that would be also one.

**Alex Hentschel**:
Yeah, I think as an initial sort of MVP, we could put that both into one, right? And say, okay, if either changes the protocol version increases, that gives us some sort of restrict of what we can do. But I agree with Jordan that that could be sort of the first step and just see how far we get with that. And maybe that's enough for the next two years.

**Bastian Mueller**:
Yeah, but not too granular because then it gets complex and we don't want that. I don't have an overview of all these different things.

**Bastian Mueller**:
I think it's really easy to bundle like all the execution stuff. We just have to like maybe from one avenue we talked about was like, oh, how do operators know what to deploy? I think likewise for engineers, when they open a PR, they have to they always have to sort of reason, oh, will this somehow break, right? Like I'm adding a new field or I'm changing the field type here, like the nature, like the encoding is different. Like you always have to sort of reason about like, what does that impact? And some, and we've seen in the past where some changes were made that had affected like components like oh the SDK is somewhere isn't able to decode that it's like so far away you can't even see it. That's the thing I'm mostly worried about but we definitely probably have to like with whatever solution we come up with like make it clear that you know PRs need to need to bump that version if they have to right and at the moment we don't do that it's sort of Operationally, we ensure that the code that's running is sort of compatible. But now we're talking about like, oh, the code itself says what it's compatible with. And I think there, we need some kind of like, discipline right because if we rely on it during operations then there's like a chance that it will curve up. I think we're talking about an emergency scheme but it's sort of an aside that we need to if we switch to that like sort of be careful that we do it and do it correctly and prevent like sort of

**Bastian Mueller**:
messing it up. I don't really have a good idea how to assess what a PR, for example, could impact. Like if I change a, I don't know, like, you know, I fix like the cadence version and I bump it up. Do I need to bump the protocol version? Yes or no? That's the question I have when I open SPR. Where do I need to change that version?

**Bastian Mueller**:
So probably we need more coordination as well between the different components and ping people and ask them, hey, does that mean that it is a breaking change? Because some things that are done in a seemingly unbreaking way and then they actually do break or make some, they end up being a breaking change even though they don't appear to be. So that's my biggest worry about this. The solution for the versioning scheme is sort of minor.

**Alex Hentschel**:
Well, it's interesting that you mention it. I'm like, my first sort of gut reaction to this is like, oh, don't we need to do that anyway, you know, with our current merge practice of does that go into master? Should it stay in a feature branch? You know, we just haven't formalized it in terms of software that the software sort of kicks us if you don't apply to it.

**Bastian Mueller**:
Yeah, no, no, it's true. It's currently, we should do this anyway, but like, I wish like, now that we are formalizing and talking about it more maybe we can also do something on that front at the same time if we rely on it even more right and say like oh this work will only happen and we do htos really frequently and oh dynamic protocol state so we we will end up I think we seem to be moving from like one compatible version to many compatible versions, software versions running out there. And so we have to be even more careful. Had to be careful, need to be even more careful now.

**Alex Hentschel**:
Yeah, unfortunately, that's kind of the downside cost of very long sporks.

**Peter Argue**:
I think there's room to add and improve on some testing as well to add gates into our CI to make sure that this version is bumped appropriately when it's supposed to be when certain things change. But yeah, I agree with Alex. This is a leap forward from where we are today. And we'll have a lot of the same problems as before, but we can take this as an iterative step to making it better. And we can continue to iterate on it to be safer.

**Alex Hentschel**:
Thank you, Peter. That were amazing closing words for this meeting.

**Alex Hentschel**:
Yeah, any last words? Otherwise, I think we should wrap it up. I don't want to take more of your time. And thank you, everyone. I'll sort of coordinate with Jordan that we write up a more concrete version and then maybe iterate with you guys on it.

**Jordan Schalm**:
More concrete version, you say?

**Alex Hentschel**:
Well, you already have a very concrete proposal in your blog post.

**Jordan Schalm**:
No, I'm just punning on the word version. Don't mind me.

**Alex Hentschel**:
Sorry, I didn't mean to go to that.

**Alex Hentschel**:
All right.

**Bastian Mueller**:
Any last words?

**Bastian Mueller**:
Can I make one proposal in the sake of our project? This is a really great discussion. Again, I don't think there's anything private about this. Just, you know, maybe there's a, was it a blog, a forum post? Maybe we can just iterate there. And like, I think people like Dennis or other people in the community, they probably also have good thoughts on this. Involve operators, like what are their needs? And, and, you know, sort of, we can come up with the best solution that we feel like on the sort of protocol side that works for us and then it doesn't work for them at all. So maybe, you know, just, uh, can maybe make this part of the working groups a bit more like this call was great, but like, we can just move it probably easily in the public and keep it operating there.

**Alex Hentschel**:
I mean, formally in my mind, this is part of a sort of top working group, right? We had that in the core protocol working group, talking about versioning, and we deferred it to a sub-working group. So, you know, great. My experience with this, though, is that unless we move that forward and sort of promote a specific solution and implement that, nothing will happen. You know, and yeah.

**Bastian Mueller**:
Yeah, we have to drive it, but I think inviting people to give feedback and doing it early costs nothing. And if no one shows up, whatever, we keep going. But nice features, Alex. Yeah, that's all. Thanks, everyone.

**Alex Hentschel**:
We'll do that. I'll copy the notes into the forum, Jordan forum post. And yeah, you're right. We should iterate there.

**Alex Hentschel**:
All right.

**Alex Hentschel**:
Thanks everyone.

**Alex Hentschel**:
Have a good afternoon.

**Peter Argue**:
You too.

**Bastian Mueller**:
Talk soon. Bye-bye.
