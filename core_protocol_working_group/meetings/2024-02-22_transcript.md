# Flow Core Protocol Working Group (2024-02-22 10:02 GMT-8) - Transcript

**Attendees**

Alex Hentschel, Alex Hentschel's Presentation, Alex Ni, Bastian Müller, Chirag Narang, Dieter Shirley, Jan Bernatik, Janez Podhostnik, Jerome Pimmel, jonny, Jordan Schalm, Kan Zhang, Khalil Claybon, Kshitij Chaudhary, Layne Lafrance, Leo Zhang, Navid TehraniFar, Peter Argue, Peter Markou, read.ai meeting notes, Sjon-Paul Brown, Tarak Ben Youssef, Uliana Andrukhiv, Vishal Changrani, Yurii Oleksyshyn, Yurii Oleksyshyn's Presentation, Андрій Слісарчук (Andrii Slisarchuk)

## Transcript

*This editable transcript was computer generated and might contain errors. People can also change the text after it was created.*

**Alex Hentschel:** All right. Hello everyone. Welcome to our first. Call protocol working group meeting.

**Alex Hentschel:** so we have many people so my thought was instead of doing a formula introduction round. Maybe we can do it each time. Somebody has something the first time they could just quickly say their name and what part of flow there associated with Yeah, so on my part, I'm Alex Central. I'm the chief protocol architect. I focus on the protocol layer of flow. And for today, I will be running this meeting. So

**Alex Hentschel:** thank you Lynne. So today our agenda is a brief introduction of the core protocol working group like our ideas on how we could organize everything then we'll talk about the upcoming priorities midterm focus and the topics. at least we want to discuss and then here about the 30-minute presentation from yurii on the dynamic protocol state which will be the foundation for some upcoming work. so we'll fill out to attendees here afterwards. I think we maybe I should just take a screenshot. So I'll take a quick screenshot to attend it and then fill that out later. Okay, so

**Alex Hentschel:** the core protocol working group so you can see my mosque. Right? So we have a readme which is just one folder app. the one link here where all the topics which are likely going to come up from our end are explained in more detail. Please go ahead and read that at some point, but we'll be summarizing a little bit or the most timely topics.

**Alex Hentschel:** Right now he and the following. Okay, but before we sort of go into the technical level let's quickly just review a few organizational aspects here. So we're planning roughly a monthly meeting Cadence. it might be more frequent depending on the topics or how many topics we have to discuss. There's the flow events and working groups calendar where all the meetings will be part of we also have the mailing list protocol at flow.com. We'll read AI as a tool to create meeting minutes and recordings and will also track the meeting minutes and recordings in this folder here in GitHub.

**Alex Hentschel:** So for technical contributions, of course, there's Discord specifically the protocol Builders channel here. Then we have our flow Forum, which I think is really great for exploratory discussions where you want some technical depths or want to discuss that some technical debts and For that we have to category builders for Builder flow core flow protocol. So yeah, and then if you have a more concrete sort of proposal of how we want to change flow or adjust some parameters that would take the form of slip a slow Improvement proposal. So that's kind of the search step from least sort of concrete to most concrete and most details. Okay.

**Alex Hentschel:** hope that makes all sense so far. If you have questions, please just jump in or raise your hand. Otherwise, I'll just keep talking here. upcoming priorities midterm Focus. So for the flow foundation and the engineering resources that the flow Foundation is contributing to flow. There are two topics that will have a reasonably high priority for the next.

**Alex Hentschel:** some months. So one is the past to zero downtime protocol upgrades. So this specifically means I'll just keep it at a high level and a couple level deal go go deeper in the next so reducing downtime. That's one thing. We also recently rolled out a new blst based cryptography stack. We're hoping that that will be able to do some block race increase performance increase as a result of that that will also be coming up here in this group. And then the third topic is recovering from Epoch fallback mode. So that essentially is one of the epoch transitions has failed currently the network goes into a fallback state which requires a spork so our Network upgrade this downtime and

### 00:05:00

**Alex Hentschel:** we're hoping to change in revises mechanisms that we can recover from a failed epox which over without needing downtime. so that sort of the most immediate priorities coming up and then on the midterm in my head, that's maybe something like six months to nine months will start thinking about permission as participation of consensus notes and the resulting bft requirements and also topic which we might discuss here is scaling the execution state to terabytes of a single snapshot plot history then So that's the high level overview about what will be coming the next few months any questions on that? Okay.

**Alex Hentschel:** yeah, so let's take a look at the sort of the topic for today. That is the pasta zero downtime protocol upgrade. So the first step I quickly describe what that is why it's important where we are right now and then that will sort of slowly go into yurii's talk where he will present the foundations of some work we've done so far which we hope to use or utilize for zero downtime. Call upgrades.

**Alex Hentschel:** Thank you Dieter for the welcoming words. so, zero downtime protocol upgrades, so first question is Why does flow have to undergo upgrade or rather? Why do we need downtime for upgrades? So? I'm very important party to remember is that flow flows protocol implementation is not fully complete. We have a fully Byzantine fall tolerant architecture design, but some parts of that design are not implemented yet. And so

**Alex Hentschel:** the shortcuts in a lot of times they just sort of fall back on human involvement. if for instance some notes misbehaves at the moment the protocol doesn't flash that notes. but we as humans can sort of step in and fill that lack of implemented Automation and so removing those shortcuts, I'll often breaking changes. and when you want to change the software and roll out breaking change you either have to make sure that your new software is downwards compatible with the previous and potentially further for the back historical versions or you just say, okay I'm spinning this as a system down and bring system office in use software image and this sort of

**Alex Hentschel:** upgrades with downtime which we previously called Sports. They have a few very important benefits over pursuing a route with downwards compatibility. So the one is that it's massively simplified the evolution off the software design right when you go to an engineer and be like, hey, you don't have to worry about downwards compatibility that simplifies their life immediately also as a result drastically reduces maintenance costs because you don't have to potentially maintain or box fix those

**Alex Hentschel:** Those edge cases or downwards compatibility sort of extra logic and it reading improves code readability. So our access is Engineers as humans to the code and that in turn significantly reduces code complexity and code in the dependency algor protocol safety. And for blockchain safety is really important. So Allowing us to upgrade the protocol without downwards compatibility. has first massively helped the evolution of flow in terms of speed but also help really much to kind of keep the entire protocol safe and make sure that we don't have a lot of sort of edge cases that we have to maintain just purely for downloads compatibility Okay, so

### 00:10:00

**Alex Hentschel:** That's the reasoning why does flow have to undergo protocol upgrades? But yeah, so as slow evolves, obviously, those breaking changes hopefully get fewer and as as sort of Engineers building the protocol also have more experience and how we can potentially evolve the protocol without needing or reducing the number of big breaking changes. and so that's the journey we're on right we started with a lot of downtime. I think last year we had something like Got it down to eight hours for an entire year. So that's 99 point. Nine two percent uptime, I think.

**Alex Hentschel:** Yeah, and so I'm very early we started with 8 Sports last year. We only had four Sparks and this year our goal is to only have one sport and I think it's important here to talk about. why it's so important for us to have one sports this year and that is because we're in that one sport. We're shipping a lot of breaking changes which shipping HP register and lining which will be

**Alex Hentschel:** A very strong optimization for the execution State and that will require some migration. I'm not sure how much Cadence 1.0 also requires migrations but there are two big evolutionary steps in the protocol which need to be shipped as a protocol upgrade. They require State migration so downtime and By not adding another Spork. We're sort of at least keeping the amount of downtime to Hopefully same similar extent as it was last year. So we're able to sort of maintain uptime numbers around 99.9% So that's the reason why this year we're kind of hoping to only do one sport is to compensate for the cost of that spark.

**Alex Hentschel:** yeah, and so

**Alex Hentschel:** So before I go on let me see. Yeah, thank you Jan for clarifying that Spork is a network upgrade. Yes. Thank Uliana. I appreciate you are here too or all our guests from the community. Thank you for joining us. Great. Let's see, are there any questions about what I've shared so far? Otherwise, I'll start going into what we currently have as mechanisms for upgrading the notes without downtime. Yes, I'll go there. Okay, so the current status quo is that we have something which we call height coordinating the upgrades for execution notes. So in short hdus and so there are few.

**Alex Hentschel:** Time I implementation limitations some are a conceptual limitations and when we talk about what we want to do better, of course, it's important for us to understand. What are the limitations of the thing we have today and so hcus at the moment are only implemented for EMS. So that is for execution notes. So that's an implementation restriction which we could change but that would require work. The second one is that and that's not a time in implementation That's more conceptual limitation. Is that height manual coordination

**Alex Hentschel:** because whenever you do a software upgrade, there's a chance that things can go wrong and by Design is an upgrade. where all the affected notes upgrade together in a very small time window. And so if things go wrong and for instance, our execution notes are all offline, then we have a problem. So we need the operators to be at least on standby during that time in case something goes wrong. They need to have configure the correct images up front and that all needs to be relatively strictly time for the hcu to go through smoothly. So that's a limitation. and the better option here would be rolling upgrade so that note operator can upgrade their note whenever they want to let's say maybe over the course of a week or some days right when they're in their time zone when they're up and awake. They can upgrade the notes and it just keeps

### 00:15:00

**Alex Hentschel:** Running so this then would require some sort of downwards compatibility. But most importantly it would require an awareness of the note of which version should I be running and which version can I be running which is kind of beyond what the hcu provides us as tooling for now limitation number three. So the hcu is Avant one time event that all the effective notes need to be observed. Meaning the protocol doesn't remember that this event has happened the protocol tells the participants. Hey, this is supposed to happen and then forget about it and doesn't force it. So in each case scenario here where our current age mechanism would fail would be that. we emit the hcu event. Let's say on

**Alex Hentschel:** on Wednesday, then we have an epochs over where a new execution no joins, which hasn't observed that hcu event announcing that software supposed to be upgraded a week later. So the end drawings later at the next Epoch. It doesn't observe that event. And as a result, it doesn't know that it's supposed to upgrade. It's software because as I said, the protocol doesn't remember it only tell Participants and they need to remember it and if there's either a box in there or just bad timing then notes will miss this u is this hcu notification? Okay, so that was limitation 3.

**Alex Hentschel:** another limitation is that u only specifies the minimum software version At a specific block boundary so a test friends. when you're at view a thousand or height a thousand you have to at least run software 1.3. and that is only safe if the software is 100% downwards compatible. So imagine a hypothetical scenario where a node operator says

**Alex Hentschel:** I know that as a block 1000. I'm supposed to run software version 1.3. I have a state Snapshot from block 500. So before that, right and the note operator could just sink. Hey, I'm boating up my notes with the newest software version and then have it catch up from block 500 to block a thousand. This is exactly an edge case that would not work with our age you mechanism because in our hcu mechanism we would say before block a You have to run a different software image and only after block or block 1,000 and higher you.

**Alex Hentschel:** You can run the software image 1.3. But we know specify what order software version is to be run and we also don't say whether it's down where it's compatible or not. And so it's easy for humans to sort of overlookses. There's no automated catching sort of misconfiguration and

**Alex Hentschel:** So there are some limitations here with the heu mechanism and that's sort of the combination of all those limitations is something that always the reason why we just don't want to take the existing each you mechanism and apply it to other node rolls, but rather want to think about the mechanism, how can we do this more stable and in a more durable way with also more algorithmic support and relying yet Less on human intervention most importantly we want to make anism that also allows us to Rolling software upgrade so that we can say within the next week all the notes should upgrade to that version. Of course that software version should be downwards compatible, but at the moment we do not have any way of sort of coordinating or enforcing this.

**Alex Hentschel:** And that will be the main focus of the upcoming work. Okay?

**Alex Hentschel:** So our short-term goals for this work around zero reduce downtime is we want to reduce downtime. We don't want to eliminate it yet. I don't think we're at the point where we actually can fully eliminate it but we want to know this will be reduced it as much as we can. so one of the goals is that we want to extend and refine the hcu mechanism to allow upgrades to all node roles. Not just execution notes. We want to focus on algorithmic updates.

### 00:20:00

**Alex Hentschel:** What I mean with that is that updates which require database migration are significantly more complex and we're already happy if you have a mechanism where we can ship upgrade that don't require a database migration. So it's sort of subset of breaking changes. We want to support rolling upgrades. So where the notes don't have to reboot in a Time coordinating Manner and we want to significantly increase the robustness of the upgrade process by making sure that we spec

**Alex Hentschel:** the protocol version that you have to run as office specific block and don't just say, it has to be at least 1.3, but we don't say that it can't be 1.5 or it can't be 1.1. So we want to make it more clear and we want to have the notes software sort of check and enforce that a little bit more on its own. Okay.

**Alex Hentschel:** We're hoping to use the dynamic protocol State as a foundation for this some of you might have heard with that we're working on this and so the dynamic protocol state yurii will talk about that. with I think the next fore We're going to ship that with an export to that. I'm Dynamic protocol State and in any changes on top that hopefully will allow us to at least get the upgrade process started. so for the next core protocol as for the next working group meeting will go into little bit more detail about how we actually want to do that upgrade process. I'm for now.

**Alex Hentschel:** What we want to do and the next half an hour is listen to yurii's talk and understand the sort of conceptual basis of what the dynamic protocol state is. So that next time were in a good spot and have all the background to discuss. what we can build on top of the dynamic protocol state who to build a software upgrades? Okay, so that was kind of the part. I was hoping to go over this meeting. I would hand it over to yurii, but before I do so, I want to make sure that all questions and questions to answer it. So any questions?

**Alex Hentschel:** No, great, then I'll stop presenting and I'll hand it over to yurii URI. Are you ready?

**Yurii Oleksyshyn:** Yep.

**Yurii Oleksyshyn:** Treatment. Thank you Alex for you for such great intern driving this meeting so far. My name is Rosary yeah, my name is yurii I will be presenting today the driving protocol state.

**Yurii Oleksyshyn:** I am a staff engineer here at 12 Foundation. I'm working on the protocol development. mostly previously it was mostly consensus now. It's all kind of stuff which is protocol related. Yeah, today's topic will be the denial protocol state which is an extension to what we previously called protocol State. We will go over the details today. Of it see what we had before what we have shipped well to the master Branch right now. It wasn't sport yet and see some development what's in future for Designing protocol statement how it will be extended and used for the zero downtime upgrades. Let's get into it.

**Yurii Oleksyshyn:** So first, I would like to talk a bit about the protocol State What we call a protocol state is basically and abstraction which allows us to get a bunch of data from previously posted blocks. so first of all, it maintains identity table. It's like a big table of all identities that are allowed participate in the current ebook will be able to participate in the next ebook or what or where participating in previous one.

### 00:25:00

**Yurii Oleksyshyn:** It is part of the protocol state. It also gives access to the blocks. We can query blocks by ad. And by height, we can query only the finalized blocks and by ID any block that was added to the chain, even if it was previously orphaned in one of the forks. It also takes care of tracking the chain finality and ceiling stages of forks. What I say forks. I mean blocks that weren't yet finalized.

**Yurii Oleksyshyn:** and it provides access to the global parameters of the chain. Such as what we have for instance Epoch commitment deadline and another stuff there. the parameters that they're saying for all participants of the network. Yeah. this is what we Define as a destruction, which is called protocol state.

**Yurii Oleksyshyn:** So it has some limitations though. as how it was implemented in previous versions. it was very stated. Basically it didn't change the information on block basis. And basically it was almost fixed for the lines of the holy book strictly speaking the identity table was changing but it was changing only three times per ebook or two times even yeah when the faces were changing

**Yurii Oleksyshyn:** But for majority of time when blocks were changing days to the protocol state were possible. sorry not the protocol state but identity table which was part of the protocol State and identity table is very important since it determines who is allowed to participate in the network. and one other limitation was that it wasn't quite suited for the light clients. It was hard to build snapshots of any block because we had to ship lots of information that was kind of disjoint in the network in our implementation. So that's what we're trying to solve with the denial protocol state.

**Yurii Oleksyshyn:** So we have a small example Blocks are progressing in use and basically if you work to query the identity tables have shot at block it would be the same as it in an number of blocks here basically, so I want to show here that no dates were supported to that and it would yield the same snapshot that as it was some other block which is kind of acceptable for our

**Yurii Oleksyshyn:** for things that we want What we would like to support in future real features. We would like to have self ejection. This is a process where an old for instance their private key was compromised and they would like to be injected from the network. They could provide a request that they would like to be excluded from the identity table and such notes will be ejected. this is called self rejection and with effective protocol State we couldn't Implement that with the dynamic protocol State we have means to do that.

**Yurii Oleksyshyn:** slashing is a process of penalizing and notes that are trying to make some business in Moose in the network if they're trying to make some offenses they could be When other notes collect proves that they have misbehaved they could start the slashing process and in the end as an outcome of that process, we will be able to exclude the note from the identity table and stop it from further participating and taking their stake. Most likely.

### 00:30:00

**Yurii Oleksyshyn:** Yes, and we would also like to have some form of Dave's to the parameters that Global Network and all participants share that to be more flexible configuration.

**Yurii Oleksyshyn:** So What we would like to have is that at some block. Our desire did you have to have this at some block? We query the snapshot then in next blocks. we see an identity update event. Let's say someone was ejected or someone with slashed and if we query later, We will have a new updated snapshot which will have the updated information there. this is what we are looking for would adding of the demand protocol state

**Yurii Oleksyshyn:** So if you characteristics of that there are protocol State it's for career, so it doesn't wait for the finalization. It's tracked for each block that was added to the chain. specifically

**Yurii Oleksyshyn:** for each block it has its own Jerome Port. it has its own version of the protocol state. they could be the same version If no updates has happened to the state, but technically it could be unique state for each block.

**Yurii Oleksyshyn:** It allows to change the identity table when identity change events. It is a completely bft. So all replicas that observe The Preserve blocks, they perform validation the diet protocol State and they specifically agree on they stay they check if the updates that were applied to their protocol state if they are valid and they are the Updates that the leader has proposed.

**Yurii Oleksyshyn:** It is since it is for each block it allows to build complete snapshots with all the information for each blog so you can credit any block and get a full snapshot with identities which are available and not ejected at the Block Which is very powerful.

**Yurii Oleksyshyn:** so we have the lowest layer schematically Everything works with the blocks. The information is distributed using the blocks. We have the blocks on top of that we have the denial protocol state which takes the information which is distributed in the blocks process that and on top of the denial protocol State we can Implement other features like BT snapshots Global parameters session or self-ejection. To it serves as a foundation that we build on the base layer of our blockchain and allows to add more sophisticated features.

**Yurii Oleksyshyn:** Let's talk a lot. Yeah, that was very high level over you now, we will Deep dive a bit deeper and talk about high level implementation of the dying protocol State how each node implements that and why it works. So we use approach with the state machines to model and implement the denial protocol state. and all updates to the state are happening using ition The transitions are implemented what we have we have basically affinite number of states in our system that we can possibly enter. during the epoch and we have fixed the number of transitions between those States. I will show more Graphics in next slide, so don't worry about that.

### 00:35:00

**Yurii Oleksyshyn:** why we have chosen this approach because

**Yurii Oleksyshyn:** it's very sensitive stuff. And it's very important to implement this correctly because processing ebook events or processing identity changes directly impacts safety and liveness of the chain. And the more robust is the implementation the safer is basically the chain so to be strict as possible. We are using this state machine approach where we Define strictly What possible transition we have? And what possible States we can enter? To it. we have

**Yurii Oleksyshyn:** yeah, that's a graphic which we will discuss here a bit how it's implemented. So here we are considering a happy pass scenario where everything goes well.

**Yurii Oleksyshyn:** So our state machine in the epoch can be possibly in four states for current ebook. Let's say we are starting the ebook and we are in this taking phase. next ebook has not been set up yet. Because we haven't observed any events only allow transition from that is to observe this citab event. And transfer the state machine to the setup phase. For the epochan when we are here, it means that the next ebook has been set up but has not been yet committed. ready yet and Then only possible transition from this state is to the Commit phase happens the same way by observing the Commit event, and then we enter the commit phase for epocan.

**Yurii Oleksyshyn:** It means the next Epoch has been set up and has been committed at that point. Nothing can stop us from transitioning to the next ebook. And whenever it's time to do that, we observe an event that we have entered the first view of the next ebook. we will move to the second phase for ebook plus one effectively confer finishing the transitioning from ebook and to ebook plus one. that what happens with the so-called Epoch State machine. which coordinates the identity table across the epochs?

**Yurii Oleksyshyn:** We also have a separate State machine for the changes to some concrete identity. So it's a lot simpler than this one. And it basically allows one observing event that ejects notes X it will set the flag ejected effectively ejecting the notes

**Yurii Oleksyshyn:** so how to read this diagram it's a bit complex, but I will try to explain this technically speaking. We have multiple identity State machines. for each state so as we have identities as many as we have state machines for those identities and each of the epoch states can have basically multiple identity State machines what that means in practice that

**Yurii Oleksyshyn:** It doesn't matter in which state we are staking setup or commit doesn't matter. we can still process any number of the identity operations so doesn't matter what is in the epoch State machine? It always our nine protocol State always allow us to eject the identities. That's kind of the takeaway from this slide that we have two State machines and they work together one with another. as I said so basically I made a title that it's a hierarchical state machine because every state of the epoch State machine is actually a state machine itself, which contains multiple State machines.

### 00:40:00

**Yurii Oleksyshyn:** So it's like a hierarchy of State machines in fact.

**Yurii Oleksyshyn:** Yeah. Let's move to the next slide. that we were talking about the happy pass we also have separate definition for them for the epoch fallback mode just to remember Epoch fallback mode is a special operating mode for the network for the protocol when we couldn't set up next ebook and we enter in this special mode where we were human intervention is needed to recover the chain because we couldn't make natural progress.

**Yurii Oleksyshyn:** So the epochful back. Mode processing State machine is a lot simpler, since it doesn't support you can only enter the ebook fullback mode. You cannot leave that mode without human interaction and k. So basically you don't have any transitions. You're always in the same state. but you can still do their idea ction. So as you see the epoch fallback mode State machine has only one state but it still is a hierarchical state and it allows multiple changes to the identity. So whenever we process and identity ejected event, we are updating the same state of the epoch State machine but different states of the identity table.

**Yurii Oleksyshyn:** It's very simple right now. But in future we are developing an initiative to leave the ebook fullback mode. without a spark and the implementation will be built by the denying protocol state.

**Yurii Oleksyshyn:** Will be supported by the demo protocol State and it will extend this protocol State machine this state machine for sure.

**Yurii Oleksyshyn:** Yeah, let's get to the next one. So we have talked about. Happy pass processing State machine and the ebook fallback mode processing State machine and I mentioned earlier that we allow only one way transition. So let's take a look at the possible flow which will lead us to the ebook fullback mode. so for instance we started the historical state of the happy pass processing State machine. let's say we are in the stacking mode. So we observed that the next ebook has not been set up yet and we get to the stacking phase.

**Yurii Oleksyshyn:** instead of we have received the epoch setup event and instead of getting to this phase the epoxywe and was not valid by Enemy by some means it was invalid. We will completely abandon this state machine and move our execution to the ebook fullback mode. basically driving all the updates through this state machine in future.

**Yurii Oleksyshyn:** This is another lab. in our implementation. We allow only one state machine or the help pass mode or the epochful bug mode to exist at the same time. They cannot work together. So If I'm even happens, we will just enter the fullback mode and process all events using that one.

**Yurii Oleksyshyn:** And yeah, and for now we will never get back to the Happy pass processing State machine as stated here.

**Yurii Oleksyshyn:** So we talked about events. A lot, but we haven't talked about how they are delivered and process by the notes. So this slide? the

**Yurii Oleksyshyn:** events are originating from the execution State execution. Notes are forming this gution results. And in the execution result, they embed Service events, which could be different kind of events. Basically previously. We supported Epoch Service events, but now we are looking to support more Service events specifically for the identity changes.

### 00:45:00

**Yurii Oleksyshyn:** So they are generated in the execution node and deliver it in the decision results, which are that included in the blocks. This way they are they form order preserving sequence. And they will be delivered to notes to the protocol state in the order. They were emitted by the execution notes because they are distd in blocked and they have a specific ordering. It's important to understand that this process is not instant tennis in any way. It's by its nature so why it's a synchronous because the past through from generating the event and delivering it to the protocol State takes multiple blocks on average. it must take multiple blocks because

**Yurii Oleksyshyn:** let's take a look at this diagram. So at the Block AI we embed the incorporate execution result which contains the identity table changing event. Then it needs to go. verification and ceiling verification and ceiling take place in the next blocks and using the same mechanism as for the execution results, they will be delivered but eventually it Block B will be created which will contain a seal for the execution result for block a Which containing the identity table changing event? only after dispatching this block. Will be which has the seal for the execution result we can.

**Yurii Oleksyshyn:** we can say that the block was executed verification notes have checked the validity of them of the block. Consensus notes have sealed it and only that It's safe to use it by the notes.

**Yurii Oleksyshyn:** So we have talked that we need to create a seal product for the diff execution result, which will hold the service event in it. Okay.

**Yurii Oleksyshyn:** So what happens next? After the execution result has been sealed. It will be distributed to the network in blocks. The block will be synced to any notes. by the consensus follower For the consensus notes, it's consensus participant but for father notes, it without loss of generality we can say it's follower. protocol cases

**Yurii Oleksyshyn:** so we will perform the validation of the block by the consensus layer if it's a valid block. Or from consensus point of view then we'll submit it to our Appliance layer is basically we check everything what was not checked on the consensus layer. Mostly mostly those checks are related to the content of the block to develop payload itself.

**Yurii Oleksyshyn:** The payload itself has we get to this part. The pillow itself has multiple stuff like sales results receipts Etc. We are interested. In this case in the Seals All seals are extracted from the Block and forwarded to the design protocol state. where they are processed generated well, and after the processing we will generate changes to the storage system and together with the blog. We will save everything to disk and at that point we can say that the blog was successfully also another executed processed by the compliance layer and it will be added To the January it can be queried later at that point. the denying protocol state will update itself and allow query and information based on that block.

**Yurii Oleksyshyn:** And the local required from the Block storage as well. again this light represents everything which happens in each node when processing a block.

### 00:50:00

**Yurii Oleksyshyn:** So what happens in the development protocol State itself when it takes a seal or a list of seals and what it does with it? We have previously seen some State machines. So events are extracted from those seals their pass to the state machines. So We create a processing State machine depending on the change State on the parents chain stage. So we chat what was in the previous block If the previous block was successful happy pass everything is good. Then We'll create a happy pass processing State machine and we'll process each seal by applying it to that state machine. We'll try to make some transitions.

**Yurii Oleksyshyn:** If it was an APM case, we have entered VM then we will just continue with that and for each next block. We'll just continue creating EFM State machines and feed all the events to it.

**Yurii Oleksyshyn:** after What are the processing of events we will take a snapshot of the resulting that denying protocol state after applying all updates? Which is called the protocol State AI ID in our case, and we will ensure that the resulted protocol state is equal to that to the one that was provided in the blog payload. This is very important step because this ensures that all replicas in the committee. they reach consensus on changes. So basically leader when he creates a block. He says this is the expected protocol state ID when you will apply changes that I am proposing. You should get the same one. and by ensuring that we

**Yurii Oleksyshyn:** we we will give a big guarantee that all replicas are applying same updates to their chain effectively reaching the same state. Which we are interesting in. We don't want a situation where the state of the protocol is diverged.

**Yurii Oleksyshyn:** What the damn protocol state is useful for clients? so as I said previously the name protocol State impacts the snapshot creation. And it gives some use useful information on block to block basis. So it provides information about the current ebook and that's ebook.

**Yurii Oleksyshyn:** A given block it also provides information about the identities that block so the client will be able to know what identities were ejected and what audiences weren't and that at that point of time. You go. It also gives access to any protocol parameters that are stored as part of the state.

**Yurii Oleksyshyn:** interesting enough that for the light clients that I am protocol state is very useful since with making a few extra queries it allows to get a trustless snapshot at any height with would making a few extra calls, but you don't need to just think the whole change verify the validity of the snapshot which is very strong.

**Yurii Oleksyshyn:** it helps to resource usages of a lot and you don't need to trust any provider to that it will say to you. this is a valid snapshot. Just trust me you can do the verification without. Don't think the whole chain. Yeah, I will be moving a bit faster. Sorry, I see we're running out of time. I still have a few slides.

**Yurii Oleksyshyn:** So the design protocol state is a foundation for. Features that we have previously discussed and we are bringing a new feature to it, Which is a distributed storage of key value entries. It it has a predefined schema of pairs that we are supporting and it can be extended of course, but we need to undergo and I'm great for that.

### 00:55:00

**Yurii Oleksyshyn:** it is designed to be used.

**Yurii Oleksyshyn:** To be used with the dragon protocol State and we are planning to use it for the version for the protocol upgrades for the first implementation. Right. Now. The story itself is let's say let's take a look at this model. It has a version and it has key value pairs. we have the version of the storage itself and many arbitrary data here. I have used to have the protocol upgrade version which block to update and what version should be said. We also have the extra flag in real estate transition attempted. This is purely ebook related stuff to track the year from State.

**Yurii Oleksyshyn:** But I'm just showing that any kind of data can be stored here. the main features of the key value store is that it's Backward Compatible by Design so we can use it in the upgrades. And consensus committee. Must reach consensus on the content of the key Value Store as it is part of the protocol state. it means that all changes apply to the key value store. They are safe they're bft and they will be the same for all notes. Otherwise, they will not accept the block.

**Yurii Oleksyshyn:** So the we said we use the same approach with the key value store with the state machines to implement the key Value Store. basically it's very simple it You can change the property with the key to some value V and that's One transition. The only thing is that I'm kind of showing it simplified where we have one property. But if you have five properties in the

**Yurii Oleksyshyn:** in the state machine You have 25 States, right? So it's actually a state machine for each property of which is stored in the quilty store. So again, a lot of State machines a lot of states. But simplified it could be translated represent this very simple. You have one state it will be changed when we will see an event which update the value. or that key

**Yurii Oleksyshyn:** Yeah, I have still two slides, but we can probably skip them.

**Alex Hentschel:** We could do is that I mean, I think yurii got the video important Concepts you already talked about so we could let the people go who need to go and just record the last two minutes for anyone who wants to catch up.

**Yurii Oleksyshyn:** Yeah. I will continue. Yeah.

**Alex Hentschel:** Okay, yurii, go.

**Yurii Oleksyshyn:** Please join.

**Jordan Schalm:** Wrong button, go ahead.

**Yurii Oleksyshyn:** Yeah, so by adding the key value store it. Changes a bit the semantics of the protocol state ID that we had before a previously we had on the kind of one big state machine we were applying changes by adding the key Value Store. Suddenly we have one more state to keep track of.

**Yurii Oleksyshyn:** what happens is that the same diagram as we had before we are receiving the block the block has seals we extract events from those seals. and start applying them to the state machines. But now we have separate events for the epoch State machine and separate events for the key Value Store. And the name protocol State basically chooses what events to apply to what state machine and the resulting snapshot of the denial protocol state after applying all updates is Combined state of different sub modules of the Divine protocol state. So we have Epoch state ID. We have the identity state ID. We have the key Value Store ID.

### 01:00:00

**Yurii Oleksyshyn:** actually store State idea which together there has together and they form a protocol state ID, which is the estate commitment to the protocol state after applying all the changes that were in that block. This is a stock before this is essential for BFD guarantees of the Chain including all the changes into the protocol state ID. We can be sure that all notes have applied the same changes. And they are in the same version.

**Yurii Oleksyshyn:** this structure it's not similar but in future it can be mercalised. to give more freedom to the clients where they would like to sing only parts of the design protocol state for instance, but still be able to verify the data. which is very very useful and potentially

**Yurii Oleksyshyn:** So we were planning to use. Yep. please

**Dieter Shirley:** Yeah, sorry for interrupting. But I'm curious it sounds to me and forgive me for not understanding the details of this but it sounds to me like you had sort of a data structure which represents the protocol State and that sort of what exists today and then we want to add this key value store that is going to allow for the storage of all sorts of potentially interesting data. Are we migrating a bunch of things that were in that old protocol State into that key value store. Could we even potentially migrate all of that data that was in the protocol State into the key value store. So there's sort of one merkelized data structure that we can look at. I see smirks from both Alex and yurii, so I feel like I'm not suggesting anything you haven't discussed.

**Yurii Oleksyshyn:** Yeah, technically you can do that. The only thing is that the initially implementation is quite simple with the cable. You store. That the second problem is that The epochs and identities are fairly complex in terms of Transitions and how to set up them. So I haven't come with the way properly to generalize the key value store to a place where you can apply any kind of data to it and to have any kind of post and pre-processing to the data which is kind of needed properly to properly handle those cases, but generally it seems that it's possible the future at least

**Dieter Shirley:** Great. Thank you.

**Yurii Oleksyshyn:** so we are planning to use the key value store for the first version of the zero down time of grades. I will just give if a simplified example of it how we were planning to use in the next slides, so if you don't think yeah, please Alex.

**Alex Hentschel:** Hey, maybe we should do that example next time, because that's actually kind of what we're thinking about or the discussion. We want to get into How can we use a key value store for the upgrades and it might make sense to take a little bit more time for that in the next presentation,…

**Yurii Oleksyshyn:** Great.

**Alex Hentschel:** because then it's both fresh and also not rushed.

**Yurii Oleksyshyn:** Yeah, okay. Yeah makes sense. Of course. Yeah, that would be it…

**Alex Hentschel:** Thank you.

**Yurii Oleksyshyn:** if you have any questions, please ask.

**Alex Hentschel:** All…

**Yurii Oleksyshyn:** Thank…

**Yurii Oleksyshyn:** Thank you.

**Alex Hentschel:** Sounds like there are too many questions.

**Alex Hentschel:** Yeah, so this is a complex topic I'm sure We'll get a better feeling, once we start working with this but ultimately it took us quite a while to really figure out how to do that in a safe and sort of maintainable way. So yeah, there is a decent amount of complexity in there. do we have a question? No, then I would like to thank everyone for the attendance today and looking forward to the next meeting and we'll put the announcement in Discord and thank you, everyone.

### 01:05:00

**Jan Bernatik:** Thank you.

Meeting ended after 01:07:17 👋