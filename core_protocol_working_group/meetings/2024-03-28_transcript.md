# Core Protocol Working Group, March 28, 2024 - Transcript

**Attendees**

Akos Erdos,
Andrii Diachuk,
Giovanni Sanchez,
Janez Podhostnik,
Kan Zhang,
Khalil Claybon,
Kshitij Chaudhary,
Navid TehraniFar,
Peter Argue,
Ramtin Seraj,
Sjon-Paul Brown,
Tarak Ben Youssef,
Uliana Andrukhiv,
Vishal Changrani,
Yurii Oleksyshyn,
Andrii Slisarchuk


## Transcript

**3:04 - Alex Hentschel:**
Hello everyone. Welcome to the Core Protocol Working Group. Thanks for joining. So today we have a pretty packed agenda. The first thing we want to do is continue on our topic of zero downtime protocol upgrades. Then we'll have a brief discussion, or sorry, brief presentation by Yurii, sort of opening up the entire topic about protocol software upgrades, which we hope to sort of coordinate and organize using the dynamic protocol state.

**5:17 - Alex Hentschel:**
We had an entry-level presentation last time, a month ago, The next topic or the next step would then be to have a discussion on how do we actually want to do the upgrades, what does a software version mean, what does a protocol version mean, things like that. And then the third topic is tuning flows main consensus. That's a little bit subject to time, how deep we can go in either of those topics. Yeah, but let's see. So before I hand it over to Yurii, I just briefly wanted to recap the presentation from last week, last month, sorry.

**6:00 - Alex Hentschel:**
So the dynamic protocol state is essentially a framework for storing data about blocks and what a node has observed, what the state of the chain is, So you can ask the protocol state things like, oh, is that block finalized? What is the latest sealed block? Things like that. And most importantly, the protocol state also manages the epoch switch over. So from one group of nodes to the next. The old protocol state was very static. It was essentially an implementation shortcut, which could not change throughout an epoch.

**6:42 - Alex Hentschel:**
Which is not a good solution because we want to have the ability to, for instance, remove malicious nodes from the network also within an epoch. So that required a little bit more of a dynamic approach. And yeah, and so that's how the dynamic protocol state came into life. And last week, Yurii has told us how the epoch switchover works with the dynamic protocol state. Or how the epoch switch over logic utilizes the dynamic protocol state. He has told us a little bit about a key value store, which is included in the dynamic protocol state, which also the epoch switch over utilizes.

**7:29 - Alex Hentschel:**
And so today, Yurii will continue with a shorter sort of presentation. And propose or talk more specifically about software upgrades, utilizing the dynamic protocol state. Yeah. And so with that, I'll hand it over to Yurii. Stop my presentation here. Thank you, Alex.

**8:06 - Yurii Oleksyshyn:**
OK, great. Can you see my screen? I'm sharing the presentation? Yes, we can. Nice. So my name is Yurii. I think everyone knows me already. I mean, it's the same group as last time. So yeah, but today we will be talking about the faster zero downtime protocol upgrades and how it will be implemented using the direct protocol state. As Alex mentioned. So let's get into that. So let's quickly recap what we have talked last time and to have a high-level understanding of the dynamic protocol state and the components of it.

**8:53 - Yurii Oleksyshyn:**
And then we will talk in detail how we can undergo an upgrade process to the protocol. So last time we have finished on the key value store. So the key value store, it's basically a state, a state which has some data in that. It is organized as key-value relations. It has a predefined schema and it's essentially a snapshot of protocol-defined parameters. So we define them up front, we say what's there, possible candidates for that is the epoch information, identities, some flags, For instance, we have invalid state transitions, and we are including there an upgraded version to kick off the grading process.

**9:59 - Yurii Oleksyshyn:**
One of the important features of the QVALUE store is that it's protected by our BFT consensus, and all updates to it are are checked by all the replicas, and only if the update is valid to the key-value store, then it can only be applied to the state. So schematically, we can see that the dynamic protocol state is a combination of the state, which is the key-value store, and some rules for how to evolve this state. The protocol rules plus the QVALUE store equals dynamic protocol state.

**10:55 - Yurii Oleksyshyn:**
Conceptually, it can be viewed as, for clients that are using the chain or other node types, not consensus nodes, it can be viewed as a high-level storage where you can put data and you can access it on block-by-block basis. It supplements protocol data into each block, and after processing a block, it has a protocol state which is connected to the block, and you can query it to get some information you're interested in. So, yeah, as I said, Mostly, it's an additional state which is available in each block.

**11:50 - Yurii Oleksyshyn:**
And that state is evolved using some rules. But for clients, it's not very important how those rules are applied. So schematically, we can see here we have a chain of blocks. And some of the blocks might have the same state if no updates were made. The block B had some updates somewhere in between or in the block B, and it has attached to it, we have a different protocol state attached, which is reflected in a different state of the key value store essentially. Yeah. Let's quickly recap how the updates are delivered to each of the nodes, like the whole pipeline.

**12:45 - Yurii Oleksyshyn:**
So the update first is incorporated in the execution result, which was previously executed by the execution node. Then it gets through the ceiling and verification pipeline. Once it collects enough approvals, then it gets sealed by consensus nodes. And only after sealing, we can take the key value store updating event and apply the state change. So once we observe a seal for the execution result, we can safely take that update and apply it to the key-value store because it was at that point executed, verified, and sealed.

**13:45 - Yurii Oleksyshyn:**
Then each of the replicas does the following thing. We have... Inside of the direct protocol state, we have high modularization of the state machines that are applying the updates. And each of them are, well, we use a concept of orthogonal state machines, which means that we divide them the input space into data types. And each state machine exclusively handles one part of the subset. And basically, here you can see that we have like a purple, a pink state machine, which handles only pink events and updates some part of the key value store.

**14:53 - Yurii Oleksyshyn:**
The green one updates its part and the yellow one is its part. And it filters only the needed events. What it gives us is, well, first of all, if they don't intersect between each other, their execution can be highly concurrent or even paralyzed. In the best scenario, basically. And it gives us high safety guarantees that the data will be modified in a very strict way. And it's easier to argue about the safety and liveness of the algorithms when the design is highly flexible and independent in terms of data consumption.

**15:56 - Yurii Oleksyshyn:**
So this one, yeah. So to summarize, we have different types of events. Those different types of events are consumed by different state machines. They are matched by type and apply to different parts of the key-value store. Um, this, this whole design is not a concept. It's already used for the, uh, for the epochs and identities in the QA store. And we are actively working right now to extend that, to support, uh, version upgrades. Um, yep. Uh, yeah. That was the recap of the QVALUE store and what was the high-level design of it and the dynamic protocol state.

**16:55 - Yurii Oleksyshyn:**
Now we will talk more about the upgrading process. We will see what QVALUE store has to offer us. We will see what design decisions we have made and see how everyone can benefit from using the QVALUE store. So, for Kivaly store to be upgradable and backward compatible, we have made several decisions to support that. So, our storage layer operates on binary data. To avoid concrete types and avoid parsing problems and serialization, deserialization, we are operating on binary types, which has the version and binary blob, essentially.

**17:52 - Yurii Oleksyshyn:**
This way we can be very flexible in the way what data we store, and we can properly deserialize based on the version. The Kivalu store also has a generic API for querying and mutating data, so different versions of the Kivalu store can be accessed using the same interface, which is useful for developers who are using the Kivalu store. And the key value store is part of the core protocol, which is part of the follower engine. And any node that is using the follower engine, any node which follows the chain, has access to the key value store and has access to the data.

**18:47 - Yurii Oleksyshyn:**
Yep. Let's take... We made those kind of important decisions to allow the protocol state to be upgradable. Let's observe an example where how the proposed path to upgrade the protocol. This is a general scenario how the protocol upgrade might go. We have a smart contract here which creates a key-value store updating event. Let's pretend that we have protocol version 1 and we created an event to set the protocol version to 2 at view 1000. This event gets executed by the execution node, and it goes through the pipeline of the ceiling verification.

**19:51 - Yurii Oleksyshyn:**
At some point, it is sealed, and all the nodes, they will observe the seal and process the event as part of their dynamic protocol stage routine. They will evolve the key value store, evolve the state, and they will include that event to their state. Then, since we said that it will be active at view 1000, we observe block with the view equal or more than 1000, we will process that block and set the protocol version to 2. Using that, well, this flow kind of describes how how the protocol upgrade will happen.

**20:45 - Yurii Oleksyshyn:**
We will observe in details why this works and a few potential problems that we might encounter using this approach. If anyone has any questions, please interrupt me and we can discuss. We will dive into a few details in the next slides. So first of all, the key value store supports a thing which we call view-based triggers or view-based activators, which means one thing, that we can put a value. We can put an activator or a trigger into some block, and it will be activated in a view in distant future.

**21:37 - Yurii Oleksyshyn:**
The view is meant to be not an exact view where it will be activated, but rather it should be treated as a threshold. So whenever the view is higher, equal or higher of the activation view, then the event should be triggered. That's the first kind of interesting feature that the QLED store supports. Yeah, this one is not enough to implement the protocol upgrade, but as you have seen, it's part of the process. The second the second feature that is that is supported by the dynamic protocol state is that key-value store can be is fork aware by design and Each fork can have independent data in the key-value store In practice it means that Let's say we have two forks here, fork one with the block C and fork two with the D and E.

**22:52 - Yurii Oleksyshyn:**
When processing C, we have observed some misbehaving information and we have said that an invalid state transition attempted true. On other side, but still a valid block. But on other fork, D and E, we didn't have that malicious data, and the state transition attempt, it's equal still to false. So essentially, we have two forks where they have different key-value store. This is very nice by design, but again, this is not enough to implement the key-value store grades. Also, because local updates of forks means that changing a fork, basically extending another fork that we were previously extending, is it means that we need to switch to basically switch versions if we're dealing with the with the breaking up rates.

**24:04 - Yurii Oleksyshyn:**
So let's say we are using this mechanism to implement the upgrade process and we have a flag like upgrade activated. Um through here on on first fork and on second fork we we like we added block c and then uh blocks that fork gets abandoned we move to another fork and uh uh on that fork the upgrade is not activated yet but but the software has already undergo um an upgrade process and uh but the but the other fork doesn't has any information on that so um Basically, for that to work, our software needs to be able to go from version 1.0 to 2.0 from 2.0 1.0, which is hard to implement.

**24:58 - Yurii Oleksyshyn:**
So this approach doesn't work quite well with the upgrade process. Let's see what can work. So the solution to that would be to use a rule which says when we have to undergo an upgrade process, then it should affect all forks. So the trigger for the upgrade must affect all forks. Still, to implement that, we will use the view-based activation. So once we reach some specific view, a specific threshold, Then from from that point we will start using new version and even if we switch forks switch to another to another to another fork we will still Will still use the the new version So let's that like let's take a look at this example somewhere in past we have We have seen a view-based activator, which says update at view 102, for instance.

**26:10 - Yurii Oleksyshyn:**
Then we create a block A, B, and C. So the block B still has the protocol version 1. The block C has protocol version, well, the block C crosses the threshold. So at that point, we activate the protocol upgrade and set it to version 2. Super and that point we are moving to another fork and start extending from the block B Start extending blocks from the block B. So yeah, so the block D Still has the protocol version 2 since Since we said that it will that the protocol upgrade will be triggered on all forks and Yep.

**27:00 - Yurii Oleksyshyn:**
And this way, even if we change the fork, we still use the new rule. Well, we will use rules from the new protocol version. And this way, we don't have a need to switch versions back and forth. So as soon as we have observed a threshold, We activate the new version and it gets used for all blocks that will be created in future. This is nice, but it has one edge case. Let's pretend that we have a following situation. So a replica is Well, we have produced blocks A, B, C. And then we have forked with the block D.

**28:00 - Yurii Oleksyshyn:**
So imagine that we have a replica which is catching up and the replica hasn't observed blocks B and C. It knows only about the fork with the block D since it's the latest block. And in this situation, replicas that well most of the replicas they have seen the block C and they have moved to the protocol version 2 but the replica which is catching up has not observed the view base activator at block B because that fork was abandoned and but the whole But the whole committee still has moved to protocol version 2.

**28:48 - Yurii Oleksyshyn:**
And then the node, the replica which is catching up, it suddenly cannot validate block D because the block D was created with the protocol version 2. But the replica which hasn't observed the fork with the BC is still on the version 1. It has like, this design has a slight problem as shown here. What is the solution to that? The solution to that is that we must guarantee that the upgrade triggers, that the trigger affects all forks. How to guarantee that? Well, we can, Uh, we can, we can delay the activation, uh, to ensure that all forks observe a finalized trigger.

**29:49 - Yurii Oleksyshyn:**
So we can rely on finalization in this, in this case. So, um, the solution. So in this case, let's take a look on this one. If we put the ViewBaseActivator somewhere in the finalized chain, here A is finalized. I specifically marked it in blue color, so it's different from the other blocks. So since A is finalized, all blocks under A are also finalized. And if the ViewBaseActivator is part of the finalized chain, then any block that is created on top will have access to that data. So any block on any forks after A, which is C, D, E, will have access to the view base activator.

**30:40 - Yurii Oleksyshyn:**
And it can properly undergo an upgrade process. So if we circle back to previous example, here, block C, we will activate the new version. To protocol version 2. And even if that fork was disbanded or orphaned, the block D will still know about the view-based activator because it's part of the finalized chain. And the node software can see that we have crossed the threshold and performed the software upgrade at block D. Even if it hasn't observed the block C. This approach guarantees that the upgrade process will be safe.

**31:31 - Yurii Oleksyshyn:**
In practice, it means that the delay between incorporating the trigger, the view-based activator, should be big enough to to handle the finalization lag, basically. We have a similar design for epoch switchover. And in practice, it works. It proved to work correctly. And we aim to use the same approach here. Yeah. So in practice, it might mean that, let's say, we need at least 500 views. Between incorporating the event and activating the event for the grade to undergo successfully.

**32:22 - Yurii Oleksyshyn:**
Yeah. So circling back to the example that I was showing previously, we have event. We create it. Setting new protocol version to 2 at view 1000. We specifically use a view in distant future. So we have like 800 views or around that for replicas to finalize the block which contains the upgrade event or the view base activator. We go through the pipeline as we discussed previously. We incorporate the event, we apply the event to the denying protocol state at view 200. At that point, we undergo a validation.

**33:16 - Yurii Oleksyshyn:**
If the threshold is big enough for the event to be safe, if the threshold is big enough, we will accept that block. Sorry, not block, we will accept that upgrade event. And yeah, and after that, once the threshold for the activation is met, we will activate the event and undergo a protocol upgrade. Yeah, that is all that I have for this presentation. We plan to extend this framework to upgrade protocol version for all nodes. And Alex will continue with the discussion how it can be used to implement some upgrades for other type of nodes.

**34:15 - Yurii Oleksyshyn:**
Specific to them. Yeah, if you have any questions, please ask now.

**34:23 - Alex Hentschel:**
Amazing. Thank you, Yurii. First, are there any questions? I know that was pretty packed in terms of content. Yeah. OK. Any questions? That's good. All right. So if you could just leave up your slides, Yurii, I think that will be great. So I'll take notes in the background, but I wanted to sort of take a step back and look at the problem again at a higher level, and then hopefully ask for all your inputs. So what Yurii has presented us here is essentially a mechanism where we can write things into a block, including stuff like, oh, we're saying at some block early, right, like block B here, we're saying that something is supposed to happen, like many, many consensus views later, and that something could, for instance, be a protocol upgrade.

**35:27 - Alex Hentschel:**
And the protocol state here will sort of preserve this information, carry it on from block to block, thereby it's visible for all nodes who are following the chain, and all nodes when to act on it. So this is a great feature. And it also addresses some of the issues we have with the HCU style node upgrades, the height-coordinated upgrades, where it could actually happen that nodes miss those events because they were not persisted in the block. Here we explicitly persist them in the block, so even nodes that join later or don't observe a certain fork still get that information because it's just part of the block.

**36:07 - Alex Hentschel:**
I think the biggest sort of thing what we as a sort of group of engineers need to align on is the question of what does it mean, what does a protocol version mean, and what does a software version mean? So in my head, a protocol version is just sort of the set of rules which describe how to go from one block to the next, how to construct the next block. And then the software version can potentially understand multiple protocol versions. Like Ethereum is a very good example. With Ethereum, the software version understands all protocol versions starting from Genesys.

**36:49 - Alex Hentschel:**
That's the reason why they have tons of if statements in their code base. And so for us, we don't necessarily want to understand or we don't want our node software to sort of understand all protocol versions since Genesys. But maybe we want our software to understand more than one protocol version, for instance, let's say the old one and the new one. And then when it sees this trigger, it's like, oh, OK, now I don't execute the old logic. I go into the new logic. And so I think that is the sort of main challenge for us at the moment is to get on the same page on what does a software version mean, right?

**37:33 - Alex Hentschel:**
Do we just version major or do we just track major versions? Do we track major and minor versions? How do we do that? And what do we store in the blocks as sort of, yeah, what's our convention? What do we store in the blocks and how do we want to activate those, I guess, version switches? That's a discussion which I think we need to have. I'm not sure if anyone here has thoughts on this. Otherwise, we'll probably take that to a smaller group of individuals and sort of focus group, a sub-working group, and have a follow-up discussion there.

**38:16 - Alex Hentschel:**
But I'm wondering if anyone has sort of high-level thoughts on this question of protocol version versus software version, and how to version do we do major, minor, yeah.

**38:34 - Peter Argue:**
Yeah, I'm happy to be part of a breakout on this. I think from a high level, we have the protocol specific one, which is outlined here. But we also have the execution version, which is needed for execution nodes, verification nodes, and now access nodes. And they have similar but different needs. So I feel like keeping these category versions separate from the software version is going to be important. And also important to make it easier for third party teams to build custom node software and have that follow the right rules, but maybe not follow the same versioning schemes that we use for the current flow nodes.

**39:22 - Peter Argue:**
So I think like anything that's going into the block should have that more holistic, agnostic approach to versioning that's not specific to like one software track.

**39:32 - Alex Hentschel:**
I see. So as I said, I'm keeping notes. So let me try to summarize what I understood. So you're saying that it makes sense for us to differentiate between what is the version, the execution, like the execution node, the protocol version of the execution node, maybe, and have a different version identifier for the version of, I don't know, maybe consensus, and maybe a third one could be collector node, something like that. Is that, did I get that correctly?

**40:07 - Peter Argue:**
to the protocol that's being worked on. And so one protocol is the consensus protocol and how all the nodes interact with each other. And another protocol is the execution protocol. And that's like the cadence and FDM and how that all works. And there's a separation of concerns between the different nodes on which of these they need to care about.

**40:32 - Alex Hentschel:**
Exactly.

**40:33 - Peter Argue:**
Yes, yes.

**40:33 - Alex Hentschel:**
I like that. So in that sense, it would essentially mean that we have different entries, right? We have one entry which says, oh, the consensus version is upgrading at view 1,000. And then there's a different entry which says, oh, the execution version or execution protocol is upgrading at a different view. And so we will probably just put that as individual sort of key values in the key value store. And if we have three, That's great. If you have 20 different things we want to upgrade independently, then we just have 20 entries in the key value store, and each means a different thing.

**41:13 - Alex Hentschel:**
So that's great. That sounds like at least our framework is addressing part of this need here to describe different parts of the protocol. Thanks, Peter. Anything you want to add? Good? OK. I think the next, Yanis, what are your thoughts?

**41:39 - Janez Podhostnik:**
So I've been thinking about the way you version stuff and with, at least with regards to the execution version, it would be great that we respected the patch versioning philosophy. If you have a node with a different patch version running on the same network, that should be totally okay and there should be no fear of causing execution forks. But if the minor version changes, then if you run that node together on the network, you might cause execution forks. I think with that, it might be a little bit easier to see when we, at least with just looking at the version, to see what node should you be running.

**42:47 - Janez Podhostnik:**
If you're missing some patch version upgrades, that might be okay. That's probably just some cosmetic thing or a minor bug fix somewhere. I think we should respect the patch versioning, at least for the execution version. That's what I had in mind the most because I know that the most, but for the protocol version, I don't know how this reflects.

**43:17 - Alex Hentschel:**
Thank you. Let me ask you a question. So when you talk about a patch version, to me, that sounds like that the software essentially behaves the same. It does the same thing, but maybe has a performance optimization in it, or as you said, like bug fakes to prevent a crash in a certain edge case. Given that it still does the same thing, I would be inclined to say it's the same protocol version. In terms of the conceptual description of what the node does, nothing has changed. And so while if you have, for instance, a minor version change, it means, oh, the protocol behaves differently in certain situations.

**44:12 - Alex Hentschel:**
So I'm wondering, what do you see as a benefit of including the patch version into tracking the patch version also in the blocks? Because essentially it just means that the protocol still behaves the same. Yeah, does my question make sense? Not sure if I managed to describe.

**44:37 - Janez Podhostnik:**
Yeah, I think I see. Yeah, there probably then wouldn't be a need to actually track the batch version to save the execution. Version patch marker, patch notifier, patch section. Because it's irrelevant to the protocol. You can run any patch version on that and it should work perfectly fine. Yeah.

**45:12 - Alex Hentschel:**
Thank you. That sounds good. So I still would like to reserve the last minutes to briefly look at the next topic. But before we move on, can I just briefly get maybe in the chat, if you're interested in the follow-up discussion, the deep dive, to be included in the SAP protocol working group. I think that's how we call it. Can you maybe just write in the chat that you would like to attend, and then I'll make sure I'll I'll include you in the invite. We'll probably try to meet next week so that we can move fast.

**45:50 - Alex Hentschel:**
And then once the sub-protocol working group has consolidated and come up with a concrete proposal, I think we would bring that back here to the high-level working group and then review it and decide on it. All right. So we have a bunch of people. Thank you. Thank you. Great. I think now I would like to briefly move on to the next topic. Yurii, if you could stop your presentation, that would be nice. Nice. OK. And so I'll share this file here, which is also linked in our agenda. OK. Yeah.

**46:37 - Alex Hentschel:**
So this is about consensus speedup. Before we go into this, I'd like to go over a few concepts and terminology here. So when we talk about flow, the technical terms we use is time to finality and time to execute it. And I think it makes sense in this as a preparation for this discussion to briefly go over what that means. And so here in this picture, you see a somewhat simplified representation of flows processing pipeline, right? So initially, the collectors, they get all the transactions, they batch them into collections, those collections go into consensus, the consensus puts or forms blocks out of the collections, and once the blocks are formed, they go to execution.

**47:32 - Alex Hentschel:**
That's what we see here. What is important here to note is that there are actually two things going on in parallel, right? So once consensus has formed the blocks, consensus proceeds to generate child blocks. And if we have two or more child blocks, usually that means the block is finalized. But execution already starts executing non-finalized blocks. So it's in a sense speculative execution. Your CPU, by the way, does that too. If you have an if and an else branch in your code, your CPU might execute both.

**48:09 - Alex Hentschel:**
And then say, oh, now I understand which branch I should have actually gone down, and then it just slows away the other branch. And the execution nodes do that too. If they see two conflicting blocks, they'll just execute both and then see which one to finalize and throw the other one away. And so that's what's happening here. And so that's also the reason why we have two different descriptors, right? We have the descriptor of time to finality, which is solely looking at a transaction and how long it takes until it ends up in a finalized block.

**48:43 - Alex Hentschel:**
So time to finality here makes no assessment of whether or not that block has been executed, right? And the reason why time to finality is important is because it means that Once your transaction is in a finalized block, you're first sure the blockchain got it, and you're also sure it will be executed, and you know in which order your transaction will be executed relative to the other transactions who got ingested into the chain. The result might not yet be known, but at least you're confident or you're sure that the transaction is in the chain.

**49:23 - Alex Hentschel:**
So if you're just selling coffees, that might be the point where you're like, yeah, I guess it's good enough for me. The payment sort of has gone well. Okay, sorry. Let me backtrack. So time to finality, we know that the transaction's in. We might not know the execution result yet. The time to execute it means that in addition to the transaction being in a finalized block, Also, some execution nodes have committed to an execution result. So if they're lying, then they're going to get slashed.

**49:59 - Alex Hentschel:**
And execution nodes have a pretty high stake. So presumably at this point, you know, you can be somewhat sure, that's the reason why we're calling it soft finality, you can be somewhat sure that the result is correct, depending on your sort of risk, risk aversion. Yeah. So if you're selling copies, right, you know, the transactions in, you know, one execution node has said, Hey, the payment went through, you're probably good, right? And if you lose your car or you lose the payment in one of a million cases because an execution node lied, well, maybe that's an acceptable risk for you.

**50:35 - Alex Hentschel:**
If you're selling yachts or private airplanes, maybe you want to wait for ceiling. Okay. So that's sort of the context, what we're working on here. And when we're talking about speeding up consensus, we're literally only talking about this part here, right? So in context of the overall pipeline, we're only talking about speed ups that are in some subsection of the pipelines. So the speed up, if you speed up the consensus, let's say by 50%, you know, time to finality and time to execute it might speed up, but probably by less.

**51:10 - Alex Hentschel:**
Okay. So that's the first context I wanted to give. Then the second context I wanted to give is, we rolled out an upgrade, September 7th to 13th, where we switched the backend of our cryptography implementation from the Relic library to BLST. And also there were various other improvements in the cryptography stack overall, in the code tag, both on top. And that results in faster vote processing for hot stuff. We directly see that on the collector nodes. So here we see that the number of collections the collectors produce per second increased by about 20%.

**51:56 - Alex Hentschel:**
So that's great. So now you might ask, well, why don't we see that speed up in the main consensus here? So we've seen some speed up here. Do we see any speed up here in the main consensus? And the answer is no. And the reason for that is because we have this cruise control system. If you want to read more, there's the link here. So the cruise control system controls how fast each view actually is and delays the release of the block in order to slow down views. And the reason we do that is because we want the epoch switch over when new notes can join and old notes can leave, that epoch switch over to happen reliably at Wednesday at about 11 or 7 PM UTC time.

**52:54 - Alex Hentschel:**
Yes. So that's the specific time we want that epoch switch over to happen. And we would not like that to be much earlier or much later because people need to have their notes up, right? They're getting paid their rewards. They're getting nervous if they, uh, It's their reward payment for operating the node. It's like 10 hours late. So we really want this reliable epoch switch over to happen every Wednesday, 7 p.m. UTC time. And that's the reason why we are artificially essentially controlling the consensus rounds, how long they take.

**53:28 - Alex Hentschel:**
And we're making them a little bit longer. So here in this figure, you can see that. So this shows illustrates one consensus view. The consensus view starts when the leader publishes its block for that view. That's a sign where all other nodes see, oh, OK, that view has started. I'm seeing that block. That's great. Then the block goes to the other replicas. The other replicas validate it. They vote for it. The votes go to the next leader. The next leader aggregates all the votes into a quorum certificate, in short, QC.

**54:09 - Alex Hentschel:**
And then it constructs its own block. So this is the time here where the leader for view V plus one has its own proposal ready. That's when it could broadcast it, right? And that's the point where the cruise control system kicks in and says, no, we're not broadcasting it right away because that would mean we're too fast. We're just waiting a little bit, 200 milliseconds, 500 milliseconds. And we're waiting. And this wait period time is adjusted dynamically such that on average we come out with a view time which we call tau zero here.

**54:54 - Alex Hentschel:**
This tau zero, that's the quantity. So that's the set point. We as humans say, at the moment we're saying we want about one We want one view to take 1.25 seconds. And if we are faster, we'll add delay. And if we're slower, then the cruise control system will in subsequent views add less delay, so it kind of catches up. And so what we now need to do in order to make our consensus faster is kind of tune this set point, the tau zero, how long we want a view to take, or how many views we want to have in one week.

**55:41 - Alex Hentschel:**
That's sort of the equivalent problem. And we have to be careful with that, because on the one hand, we have cruise control, right, which is slowing down the system. And then we have the pacemaker, which is which is sort of abandoning views if they take too long, right? So you can very well imagine that if we mistune our cruise control system, it will drive the pacemaker into abandoning tons of views, and then our block production rate is like massively dropping. So it's a non-trivial tuning problem here.

**56:13 - Alex Hentschel:**
And yeah, so there's a very long content here in this document. Where I go over the data. So here we've seen that very early, that's about a year back. Yes, April, May. It still took us 827 milliseconds just to execute the protocol. So let's go back here. It took us 820 milliseconds on average from the time where the leader proposes a block to the point where the subsequent leader is ready to propose its block, 827 milliseconds here, right? We can't, we can't, well, we can optimize the code, but the only thing cruise controllers can do is add delays, right?

**57:09 - Alex Hentschel:**
It can't make sort of the protocol execution faster. So 827 milliseconds was about a year ago, the fastest we could theoretically run. So you see that here, 827 milliseconds. Now, a year later, this has reduced to 218 milliseconds. That's in part because our consensus committee got smaller, but also in part because a lot of optimizations went in, right? So now it takes us 800, sorry, 218 milliseconds. So meaning that here, from here to here, From one block to the next block being ready, it now only takes us 280 milliseconds.

**57:55 - Alex Hentschel:**
And cruise control recognizes that and says, oh, I guess we're running way too fast, or we're way too fast. I'm adding much more delay. So the blue histogram here is the delay we're adding. And on average, cruise control by now adds about 1.1 seconds delay each view to keep the epoch switch over at our target date. And now we want to tune those internal parameters so that we're waiting less time and making consensus faster. In other words, we're packing more views into the epoch. I would like very much to go through with everyone interested through this analysis, but I don't think that that should happen in the protocol working group.

**58:43 - Alex Hentschel:**
I think I would like a smaller group of interested individuals And then we will go through the results and sort of proposals for parameter adjustments. We'll decide on one specific set of parameters and come back here to the core protocol working group and report our suggestions. And then we can decide on it. So again, I would like to ask who's interested in this area of tuning the consensus, and then I'll invite you to a follow-up meeting. Yeah, so if you wouldn't mind just quickly dropping a line in the chat that you would like to attend, that would be very nice.

**59:25 - Alex Hentschel:**
Thank you very much. All right, cool. Thanks. I'll take a screenshot of that. Yeah, I think that is the content here for today. Thank you very much for joining. I really enjoyed this. I think we had a lot of technically packed content. I hope we get to unravel that a little bit for some of you. Thank you very much for your time. Thank you very much for your attention. And the next core protocol working group will roughly be happening in a month. And in between, we'll go into those topics deeper with the sub-working groups.

**1:00:08 - Alex Hentschel:**
And maybe, hopefully in a month, we'll have some progress on the topics back here to discuss. Thanks, everyone, and have a great rest of the week and a good weekend. Bye.
