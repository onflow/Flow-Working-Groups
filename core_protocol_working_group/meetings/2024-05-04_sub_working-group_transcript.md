# Core-Protocol Sub-Working-Group Meeting on HCU-Style Upgrades for All Node Types, April 04, 2024 - Transcript

### Attendees

Alex Hentschel, Dieter Shirley, Jordan Schalm, Leo Zhang, Peter Argue, read.ai meeting notes, Vishal Changrani, Yurii Oleksyshyn

## Transcript

_This editable transcript was computer-generated and might contain errors. People can also change the text after it was created._

**Alex Hentschel:** So I'll share my window.

**Alex Hentschel:** so this meeting is about ing. generally I should say the protocol. So the rules which we have implemented in the software. And the reason why this is important is that we're planning to only do for at least after the crescendo Spork to the next spark and 12 months. So that's a pretty long time for us to not roll out any changes revisions bug fixes stuff like that and also no new features.

**Alex Hentschel:** yeah, so that's the reason why I think it at least would be immensely helpful to have some way of upgrading the protocol and to software it doesn't need to be perfect. But yeah, I guess the more tooling we have at our just disposal the better. Okay, and so let's quickly maybe talk about this status quo what we currently have in terms of mechanisms to upgrades software. and by the way, this is not a presentation from me. I'm just trying to sort of get everyone on the same page provid.

**Alex Hentschel:** Bit of context babe, but they're all means please jump in ask questions interrupt and I'm happy to go into discussions anytime. So going back the mechanisms we currently have for upgrading software. So the main mechanism we have hcu's and rolling upgrades which are really really Limited at the moment.

**Alex Hentschel:** So with rolling upgrades we essentially can only deploy upgrades which are entirely downwards compatible and essentially all nodes in the old version are understanding What's the new version does each use are a little bit different there. We can deploy breaking changes, but they only applicable to execution notes. So that's one limitation and the other aspect which I think Vishal is much more equipped to talk about if you want to is the manual coordination which is around in hcu, Because we need to talk to the note operators. There's a really really small time window in which they have to all sort of have the new software version at least ready so that when they're not reboots it can pull that software version. We want the note operators to be on standby in case something goes wrong.

**Alex Hentschel:** and that requires just a lot of human coordination and human interaction. And yeah, so the third limitation is that the HCU is essentially an event which

**Alex Hentschel:** the execution notes only once it's included on a block it's one flag and they have to memorize that so now imagine you're a note operator. You're joining right the age or the view of the HCU has been announced in the last Epoch. it's a new Epoch. You're joining as a new epoxy. You've never heard that announcement, it wasn't online. So very good chances for us to at some point, really mess up something were just doesn't know, it's not the operators fault. It's not our fault. Just how through the cracks also not a great scenario, right? That's why we have software to have automate those things next one limitation number four the HCU only specifies the minimum software version that you need to run out of block. Right? So it says you need to run version three starting from view the Thousand. So now there's a new note operator coming in there hey,

**Alex Hentschel:** I'm spinning up my notes. this is the latest image version 3 great. I'm going to put that on boot up my execution note and have it latch have it catch up from the beginning of the sport, but guess what? Neither the notes or the node operator new that at the beginning of the sport. We only have software version or protocol version 2 not 3, right, but they're executing all the old blocks with the newest software version. They're not as far they're not.

**Alex Hentschel:** Does notice anything but they're probably producing wrong results. So by the time they've caught up they're already very far down and execution Fork also not something which the HCU mechanism at the moment is equipped to handle so there a bunch of limitations and I think they are fine for how we have used u so far right only for execution notes. It's sort of very deliberate mechanism to upgrades in mostly just security issues, right or maybe performance issues and things like that, but I don't think that really sort of or if you try to do that at scale larger number or more notes, no roles affected more hcu's I think we're sort of at least elevating our risk profile right that one of those things goes wrong.

00:05:00

**Alex Hentschel:** Okay, so I want to stop you briefly and make sure that everyone is still good their Crush other questions any thoughts that I misrepresent anything, because Vishal and Leo, you probably know best. Yeah. Okay.

**Vishal Changrani:** No, sounds good.

**Dieter Shirley:** so I'll jump in real real quick…

**Alex Hentschel:** Jordan

**Dieter Shirley:** because one of the thoughts I have around this and maybe this is exactly what you're getting to Alex but I really would think it would be good for us to be really explicit about The types of upgrades we anticipate being the most valuable.

**Dieter Shirley:** the easiest and hardest to support because to me. It's like, we can sit here all day long and say it should do this and it should do that. But at the end of the day that the truth might be that it's like look we have no plans any time in the next year to do a bunch of upgrades in that part of the software right or though upgrades in that part of the software important but not urgent and so if we have to defer upgrades to I don't know it doesn't matter. I don't want to try and think of an example right now.

**Dieter Shirley:** to some subsystem that that's fine. it's okay for those kinds of upgrades to take a while. And we always want to ship software sooner rather than later so we can be testing in production as best, and getting real-world data, but we don't need to fall over our cells in order to make sure that we can ship those kinds of upgrades. Whereas this other kind of upgrades that's absolutely our goal for the next year is to be constantly working on this and constantly wanting to do improvements on this area. And so it'll really hurt us if we can't ship any software in that area. I don't know if that's even going to be useful discussion, but That's what jumped into my mind.

**Alex Hentschel:** Yeah, I mean totally So all I'm trying to do right now is sort of get everyone on the same page of where we are right now and what tools we have at our disposal to address exactly the question. You just raised what type of updates do we want to do? of course a more General the more work it will be we haven't really started that work. We're still working on the most basic Primitives even make any sort of non-rolling upgrade possible right at the moment warrant, even there. we're working that this will ship at the spork. So if you're okay with it, the most of this meeting will be a discussion around those points and I think what you just talked about is more or less what I have here at the first point and I sort of extended that to included that to include what you just said. So if you're okay deferring that discussion for maybe 10 minutes, that would be great.

**Dieter Shirley:** Yeah, yeah. Sorry, I wasn't saying we should talk about that now. I'm just saying that's definitely a topic for.

**Alex Hentschel:** Yep.

**Dieter Shirley:** For this yeah.

**Alex Hentschel:** Thank you. And I appreciate it because that also helps me set the mindset here Where do we want to get that? Amazing. Thanks Jordan. Sorry we have been.

**Alex Hentschel:** glad

**Jordan Schalm:** Can you scroll back up to wherever you were previously?

**Alex Hentschel:** I will.

**Jordan Schalm:** I just think there's one. problem with the current HCU which isn't actually a problem, which is The third one.

**Alex Hentschel:** Or maybe I'll try to make it bigger.

**Jordan Schalm:** the Number three in your list we store the version Beacon and The latest version Beacon. So even if you boot up after yeah,…

**Alex Hentschel:** we do. Okay.

**Jordan Schalm:** we do so Just to clarify. I don't think that one is actually.

**Alex Hentschel:** Okay, I'll cross that out.

**Alex Hentschel:** start at snapshot Cool, and nice great one last problem.

**Alex Hentschel:** Great. So I quickly wanted to propose a set of short-term goals sort of in my mind. And again now, we're already sort of starting in the discussion.

00:10:00

**Alex Hentschel:** So the main goal here is reduce downtime. if he could just do Sports as much as we wanted there wouldn't be any issue. We would just do a sport for every sort of rolling upgrades or every upgrades. But of course it requires, downtime. So that's suboptimal. And so What I think is useful for at least sort of some initial version. what Peter I think you're right. We should just put this into the discussion, here I'll just put that here and go back to this part here. So

**Alex Hentschel:** Okay, so we've talked about the HCU limitations so far I quickly would like to talk or recap The Primitives that the dynamic protocol States provides us or will be providing us starting from the crescendo spark to potentially coordinate protocol upgrades and so quick recap…

**Dieter Shirley:** which

**Alex Hentschel:** what the dynamic protocol state is in a nutshell the dynamic protocol state is a framework for storing is snapshot of protocol Define parameters and supplemental data into each block so each block has sort of Conceptually a little data field. We only include the hash, but I think that is sort of An important here. So each block has a little patch where you can write in data, and it's largely up to us what we want this data to be. It's just that we need to encode it as protocol rules. So that all content is notes sort of know as of which rules you can write data patch into that space in each block.

**Alex Hentschel:** Yeah, and so you can think about this data storage ability for each block as a key value store. That's how we count largely implemented it and so you can say I'm adding let's say this value or destruct into the key value store and here's the state machine which sort of evolves what is in that respective value from block to block right each block you have to say this is my new value. It can be the old value. Right? So for instance, we're currently running protocol version three next block. we're currently running total call version 3, but you can provide a state machine that test. if you're observing a certain service event, we change this we're currently running versions three two, we're currently running version 4 so you can both store that data as well as provide custom logic to upgrading that data from block to block. So that's a framework. That's

**Alex Hentschel:** Dynamic protocols that state provides us and this framework is already used for epochs which over so it has all the notes permitted as of this Epoch are Alice Bob and Charlie here are their keys. And for the next Epoch it will only be Bob and Charlie and Eve is joining. And Alice is leaving and that is their keys. So you already kind of see I hope The rough mechanics of houses is working for the epoch and I'm hoping to use this framework also for coordinating software upgrades right to whatever extent we want our software upgrades to be. And so there are a few very minor Primitives that we have already implemented which one is a view-based trigger so you can say for instance. We're now on block a thousand.

**Alex Hentschel:** And that block 10,000 or view 10,000. I would like this new data value to become active. So either if you hit view 10,000 or we're exceeding that's threshold, on each Fork. when we're exceeding that view threshold of 10,000 will the view-based trigger essentially. It's a way to represent that something should be happening. It's future in Java if you're familiar with that. and so the important part is that the key values. the dynamic protocol State. It's core so, wait View coordinated rather. Yes. Yes view coordinates and height coordinated and so

**Alex Hentschel:** Yeah, so what's important here? Is that the key Value Store writes data into the blocks, right? It looks at the parent block then says what is in this new block as relevant content to update my values and then the resulting key Value Store snapshot is this so it's for dependent right? Each Fork can have more or less in Independence head of values. that's great. But that also means that if we are having a view based trigger it might activate in different Forks at different times or something Forks. Not at all often before they reach that trigger view straggle view. So that's the second Point here. the problem with this sort of completely.

00:15:00

**Alex Hentschel:** Pork independent notion is that it creates some complex complications when you think about software upgrades, assume you do a software upgrades and assume it requires a restart, right? When you switch between forks. You don't want to all the time switch force and back between the old version the new version potentially having to reboot each time. so that's sort of slightly mutation, which we have to work around when we use this view-based trigger that we say, maybe the protocol version can just be purely downwards compatible and then we can just depending on where each Fork is in it and it's protocol version, we can either use the new protocol if it doesn't require any reboot and the implementation can just smoothly switch between both versions, but if that's not the case for instance, we do some State migration or something like that.

**Alex Hentschel:** You reboot the notes, then we don't want to switch force and And so that means once we activate or want to reach that trigger, we have to make sure that all other Forks if they are extended they're also extended with the new software version and the way we generally do that is to say we're triggering it very far in the future. Let's say a thousand or

**Alex Hentschel:** And blocks into the future and by that time the trigger which we're now putting in one fork is hopefully finalized by it. meaning if I now put a trigger in the current block and 10 blocks later. My block is finalized. It means that every Fork which reaches that view 10,000 views higher will have that same trigger in it, right and then you can just say okay. We're reaching the trigger. We're just switching over and therefore the software upgrades. It's essentially not for dependent anymore. That's a little bit of an ones.

**Alex Hentschel:** I'm not sure if I manage to explain that really in detail, but it at least important that you're aware of the problem. that we need some sort of delay here. By the way, the execution notes already do that too. They say when you do a version Beacon event, there is some sort of safety threat holes to make sure that is finalized and only then the HCU can happen. So it's a similar concept here. Okay, I think that sort of it form for my setting the stage and I would like to maybe now dive into this area what you have brought up Peter. You have a question.

**Dieter Shirley:** Yeah, so the first question I want to understand is you talked about how there's this protocol State and it's a key value store and then you talked about how you can set.

**Dieter Shirley:** those mechanism

**Alex Hentschel:** That mechanism will ship In the next box in the Christian handles Fork the epochs which overlogic uses that it says, at this view we're crossing into the new epoch.

**Dieter Shirley:** Okay.

**Alex Hentschel:** And then we just have a different set of for instance consensus participants.

**Dieter Shirley:** And that mechanism currently doesn't have a safety on it. there is no block that says. Hey the code will allow you to set any view presumably including a past view or the very next view which could lead to chaos. And so right now the code that triggers that sets that up. Because it's only used for epochs which over that we know has a nice lead time to it. And so we're not. to have chaos at the moment,…

**Alex Hentschel:** Exactly. Yeah.

**Dieter Shirley:** but if we use this for another mechanism, then we have to be thoughtful about that as well.

**Alex Hentschel:** So the current Logic for the epoch switch over it has a similar flavor of this it's too close to the epoch.

**Alex Hentschel:** We haven't heard the epoch committee event. we have a problem, it's a different approach of guaranteeing enough lead time. that I think depends a little bit on your logic which you want to put in, for some things it might be fine. If it just triggered the next block, And so that's the reason we haven't sort of spend a lot of time really hammering out the framework. we're most concerned about providing really crude Primitives that make it possible at all and might require some engineering work to put those Primitives together to useful system. So we explicitly try to not over engineer it.

00:20:00

**Dieter Shirley:** Okay.

**Alex Hentschel:** Jordan

**Jordan Schalm:** I'm still kind of putting my thought together. Yeah, you just said something that I don't know if I agree with which is maybe it's fine for it to trigger in the very next few.

**Jordan Schalm:** because then you can have people disagreeing about

**Jordan Schalm:** when it triggers, right?

**Alex Hentschel:** Every okay, maybe so for instance, let's say we're just adjusting the timeout parameter, for this block, we're waiting two seconds and for the other block, we're only willing to wait one and a half seconds. you could presume you can do that independently on different Forks, and that's a scenario where I think you could very quickly thought up trigger the change maybe right that can't be the next block because it hasn't undergone sort of consensus verification. that not somebody some malicious notes writing garbage into the key value store and I think that's your concern So maybe it has to be all the second next block or something. That's the earliest we could trigger it and for some applications like adjusting protocol parameters like timeouts. We might be able to do that for version upgrades. We're most certainly not be able to do that.

**Dieter Shirley:** But for something like that would we even put it in the protocol state?

**Alex Hentschel:** But I mean look, we just had that discussion yesterday about addressing the timing values right from for consensus, so now imagine that all those timing values, at the moment they're hard coded by the software now imagine that they're all in the protocol State, because the protocol State can receive messages from the execution requirement through Service events, right so we could adjust the content.

**Alex Hentschel:** Timing through smart contract or through governance transactions right through smart contract the smart contract would then send the service event to the protocol State and say hey, please change your time, your hot stuff time out from three seconds to one second.

**Alex Hentschel:** So we don't even need a new software in that case.

**Dieter Shirley:** yeah.

**Alex Hentschel:** So it's not only useful in that sense, but useful intense of upgrades of software, but it's also useful and just sort of making parameters easily configurable. So that note operator Stone have to hand change them by hand, or set command line parameters that we can sort of just write them in the protocol State instead.

**Alex Hentschel:** I hope that made If it did make sense. I'm happy. If it didn't. Please let me know.

**Dieter Shirley:** I mean look I have two thoughts on that right one, which is look if it's a parameter that

**Dieter Shirley:** Doesn't matter if some nodes are doing this something and other nodes are doing and other thing then maybe it's just like we send an email and they change an environment variable and reboot. I don't know on the other hand there is that practical thing of yeah, but if we have this mechanism where we can set a default it doesn't trigger any Byzantine concerns Why wouldn't we use this because it's just easier right then having a second mechanism where Vishal has to email people and say, just set a environment variable. We're just read it from the protocol are from the execution state. So there's a part of me. That's like no the protocol State should just be these things that we need to have a consensus on But then there's a part of me. That's like, yeah, but then we have to have this other state that

**Dieter Shirley:** Isn't security dependent and now we're just creating things that are more complicated. So maybe on a per key basis. There's a key when you set the value you say this key can't be updated more frequently than without x amount of lead time or something like that. Or maybe it's a partitioned protocol state…

00:25:00

**Alex Hentschel:** exactly

**Dieter Shirley:** where these Keys over here have a particularly time and these Keys over here. No one.

**Dieter Shirley:** they're just suggested defaults or something. I don't know so there's a part of me. That's like I guess what makes me nervous is not your idea that there are some parameters that can be changed willy-nilly but that if we have a mixed store of nilly parameters and it's important. We have consensus on parameters in the same bucket. I'm working. I'm not worried that nilly parameters will get mixed with the other ones. I'm worried that those important parameters will accidentally get marked as Willy Neely updates and then we end up with chaos.

**Alex Hentschel:** Yeah, we have thought about the safety mechanisms and isolation and all those so I'm less concerned about it but in the end. If we're using this, we need to understand or everyone who is working on this needs to understand precisely what's happening. it's not a sort of simple thing. it's more or less a I don't know. It's head of power tools, and if you screw it up, you're gonna solve your hand but if you know how to use those power tools, you can build really amazing things and that's kind of the thing. I want to get across here. It's a tool This protocol Engineers, to build more complex amazing things. It's not a sort of framework which prevents us from doing something stupid.

**Alex Hentschel:** Your immunity there.

**Dieter Shirley:** I am muted. again, it's just that I don't know if you have a single I don't want to get caught up in the analogy. I was trying to get the analogy to work but I get you but the problem like this is exactly why. Look, We're all humans. I get it. We're not supposed to make mistakes. Right? But if we didn't ever make mistakes, we wouldn't need a language with type checking right? it's like there's so many things we have…

**Alex Hentschel:** Yeah.

**Dieter Shirley:** where you could argue. we don't need these protections because we're all smart and we're professionals. No, we're humans and we're gonna make mistakes and this is just one more way that we could make mistakes.

**Alex Hentschel:** Yes.

**Dieter Shirley:** but I don't think this is something that is going to be used all that often. So maybe it's okay if it has some sharp pointy engines edges and we just put our safety glasses on every time we use this tool Even If all we're doing is using this tool to sharpen a pencil once in a while.

**Alex Hentschel:** Yes, and we can add those safety mechanisms later, right? But what I specifically told Jordan and…

**Alex Hentschel:** yurii, let's not end any safety mechanisms because chances are very high. This is not going to be used the way we're intending. We've just over engineered it's a hell out of it and no one is using it, you…

**Alex Hentschel:** and if you realize and have a year we need safety mechanisms. We'll just put the safety mechanisms in or maybe the next in a year.

**Dieter Shirley:** I type annotations later now. I think that's right in this case,…

**Alex Hentschel:** exactly Okay.

**Dieter Shirley:** but I get you I get you.

**Alex Hentschel:** Okay, cool.

**Alex Hentschel:** Yeah, so I think now is exactly the time to talk about what type of upgrades do we want to want to support so my gut feeling is that we want to do some we so alright say that so what would be ideal is a scenario where we could do something like an hcu, where notes need to pull a new software image and we could tell the operators. Hey, please load that new software image on your node any time next week and then the new protocol in the software will activate it according view. what I mean that we kind of decouple this activation of the new software from deploying the new software because that would remove all that coordination work Vishal has to do

**Dieter Shirley:** Not yeah, and actually a Bitcoin goes even farther than this. I don't know if ethereum goes this far but Bitcoin I'll go even farther than this where it's like

**Dieter Shirley:** Each node in the network it in the past will say whether or not it's running that new version of the software and the switch over won't happen until a critical mass of nodes have indicated that they are in fact running that new version of the software. Right? And so you could have a thing…

**Alex Hentschel:** Yeah, we could add that.

**Dieter Shirley:** where it's not just yeah, next week all the software's gonna upgrade and you have a week to update it could literally be the protocol will not change versions until we've seen that two thirds of people have positively indicated. Yes. I'm running I'm ready for the new protocol upgrade. I think that's the far end. I don't know if we want to do that, but that's the far end of I think where we could go.

00:30:00

**Alex Hentschel:** Yeah, my feeling is that if you find that sort of so how I understood what you just said is that we coordinated by hand and tell the note operators. Hey, you have to put the new software version in over the next week. And then let's say on Friday the new protocol that activate, that's that sort of this coordination by hand. Right and then the next step would be to automate this coordination. So does that make sense?

**Dieter Shirley:** Yeah, Right I think the extreme end is

**Dieter Shirley:** we put out a new piece of software and it's available to any node operators who want it. we through blog posts emails, whatever we let it be known that this new version of software exists. But we have absolutely no power other than notes operators ourselves to dictate when that takes place. It's just as soon as a critical mass which we can Define as the developers is hit then the next Epoch or whatever time frame is when the new version of software takes place and then we don't know maybe it takes place in a week because everyone updates their stuff immediately and the switch over happens next week. it never happens. Maybe it takes six months right like that. That would be the sort of the extreme decentralized version of this would be that I don't know if we need to go that far. I just want to make sure everyone sort of understands that that's sort of the far end.

**Alex Hentschel:** Yes, yes.

**Dieter Shirley:** of what I think is possible and potentially desirable

**Alex Hentschel:** I would strongly advocate for not going that far, for only having this sort of predefined trigger at a certain point and giving the node operators a week to roll out the software at their own pace to their notes that sort of at the first milestone.

**Dieter Shirley:** That so again, I don't want to talk about what Milestones are or whatnot. I'm sorry. He said that and then you added at the very end as the first Milestone. hundred percent.

**Alex Hentschel:** Sorry, not my phone first thing.

**Dieter Shirley:** There's no way that's our first Milestone.

**Alex Hentschel:** Yeah. Yeah.

**Dieter Shirley:** Yeah. Yeah, there's no way.

**Alex Hentschel:** No, I meant how do I say that, in my head when I'm thinking about sort of software engineering I'm thinking about stocks that we want to get eventually into what's currently going on and things we shouldn't be worrying about and to sort of this automation how activation is to if enough node operators have to pull out the new software. That's something I would propose not to worry about for now.

**Dieter Shirley:** so I agree with the caveat that it.

**Dieter Shirley:** If it were easy it removes so much stress like you saw Vishal like I couldn't help himself.

**Alex Hentschel:** Yes.

**Dieter Shirley:** No, we're gonna set it a week from now or we're gonna set it two weeks from now, but for that whole two weeks, we're dang. what if they don't update in time my God, have you noticed the coinbase ones aren't running the new version yet, what happens which right and we're just coding that away. so again, I'm definitely not saying this has to be a feature we're building forwards,…

**Alex Hentschel:** Mm-hmm

**Dieter Shirley:** but I also feel like y'all need to be aware of the stress that's gonna take off of the ecosystem and off the foundation, Suddenly It's not the foundations responsibility at all as to when this stuff rolls out and there is no possibility the network goes down because some people rushed and some people

**Dieter Shirley:** We're slow, it has to be super majority consensus. So again, I think To me the bump that I don't know that we're going to be able to cross anytime soon is can we have a version of the software? That supports two protocol versions without a reboot or at least with a very quick reboot. That's the bump that I'm worried.

**Alex Hentschel:** Okay.

**Dieter Shirley:** Once we're over that bump. I'm not sure that this mechanism is Like is the bridge too far. Do you know what I mean?

**Alex Hentschel:** Yeah. Yeah. I appreciate you bring that up. And I want to be absolutely honest about it in that this framework is not going to help us with what you just said, the big bump being able to have the protocol or the software support for two protocol versions. This framework is not going to help us at all with that.

00:35:00

**Alex Hentschel:** That's the case-by-casing, we've set.'s just because in I don't know how to do that, and The only thing I can say is hey when the first time comes up, let's look at the problem and let's see if we can make that, super have it support two versions maybe with an if statement, right? Or maybe we say, it needs to reboot we need to do some State migration or no, we can't it needs to go to the sport. Right? And I think this is so Case by case dependent that I think any attempt from us to put that in the framework without having undergone many of those Sort of updates by hand first is just going to end up in over engineering.

**Alex Hentschel:** So yeah in the end, what I would Define the work of Jordan in yurii to be a success is if one of you Engineers comes up and say hey. I would like to do an HCU style upgrades for I don't know consensus notes or access notes. I know how to do the logic but I don't know how to coordinate it. Can you help me coordinate it and…

**Alex Hentschel:** then Jordan and yurii say yeah, no problem. We can coordinate that with the protocol date in this way. then I think we have already made a major Milestone, Not that we can solve any upgrades but we can at least do some upgrades. Does that resonate with everyone here? Yeah, okay. Great. Vishal

**Vishal Changrani:** Alex can you dive into a little for the first part where someone comes up with saying that they can do the upgrades? They can modify the notes software to manage both versions. Is that correct? Or?

**Alex Hentschel:** For instance, It could be that I'm sorry Leo I'm using you as an example here. let's say Leo says hey Alex we want to do. I don't know.

**Alex Hentschel:** Collector notes, right we want to do collector notes. I know what I have to change in the logic, that's a logic can run the old protocol version and it's a new protocol version right? But I don't know how to get all the notes to sort of coordinate and load that new version activated at the same view. Right? Because if all notes can do the old version and all notes can do the new version. That's great, but they still need to call makes that switch, all at the same time and that's a hard problem to coordinate that And yeah, and then I can tell Leo. Hey, it's great that you have figured out the version of sort of the logic right on the higher level logic to go to Jordan and yurii and talk to them how to use a protocol state.

**Dieter Shirley:** So you're not saying hey. You can't have a version of the software that supports multiple protocol versions. You're just not requireing it and…

**Alex Hentschel:** exactly

**Dieter Shirley:** and what you're saying is look like I don't know exactly what happens on that, when that view happens, but I can guarantee you that everybody will agree. That it's time, right? So…

**Alex Hentschel:** Exactly exactly.

**Dieter Shirley:** what you do at that time?

**Alex Hentschel:** Yes. Thank you.

**Dieter Shirley:** That's up to you and the nature of the change you're trying to make but knowing that it's time I can help you with that.

**Alex Hentschel:** Exactly. Yes. Can you help me write that down in a keyboard here Dieter?

**Dieter Shirley:** I don't know. I just said it would be recorded.

**Dieter Shirley:** Right here. Let me see if I can put something in there.

00:40:00

**Alex Hentschel:** Amazing. yeah, I'll add oops.

**Leo Zhang:** I add something at the end of the dock which is related to the question. I'm going to ask but I'll let you guys finish. this first

**Alex Hentschel:** Thank you.

**Alex Hentschel:** Okay. Thank you Dieter.

**Alex Hentschel:** Okay, do you want to ask your question?

**Leo Zhang:** Yeah, I'm still organizing myself. Sorry if my question.

**Alex Hentschel:** or good

**Leo Zhang:** Would yeah, so I think at the beginning you discussed how to use a signal to send out an indicate stuff. I want to take a step back and just to categorize different scenarios. For example, let's think about why do we need pork? And the whole point here is to get rid of the sport and…

**Leo Zhang:** we can upgrade without a spork why we need Sport and there are a few cases. The first case is whether we want to stay in my equation, right if Yana says, we need to fix something in the execution state for example, We need to stay the migration and whatever we do we have to wait for the executional to finish the migration which is slow and we cannot

**Leo Zhang:** and we have to wait for the execution because we have to wait for the migration because we need the new root hash to be included in the next block. That's why we use pork with Spork we can say okay, let's say in the previous book block 100 is the last sealed block and starting from height 101. We are gonna start with a new root hash and that is a migrated for the migration state. So In the best scenario, let's say we get rid of sport right maybe consensus node. We are just going to introduce this upgrades. Let's say consensus node can still keep building blocks, but we

**Leo Zhang:** but we have to wait for the execution notes all the execution or to finish the state migration and somehow We need to replace the latest state. Route hash into this new State Route hash, which we don't have a mechanism for this So right now and I don't think we have designed anything for this year. It means if we ever have a state migration then a sport is required. and this is something maybe we need to install as Right is if a state migration is involved, how can we

**Leo Zhang:** how can we do this high quality upgrades such that? the consensus now can still keep running and still be able to switch the state root hash and this is the first case and second one is that

**Alex Hentschel:** I'm Leo before you go on is that your 0.5 here the one you just described.

**Leo Zhang:** Just yes.

**Alex Hentschel:** Do you mind…

**Alex Hentschel:** if I move that up?

**Leo Zhang:** Okay. Sure.

**Dieter Shirley:** Okay. I don't know…

**Leo Zhang:** Yes. …

**Leo Zhang:** that's either.

**Dieter Shirley:** if I should interrupt or not because I think you're concerned about exactly the thing that Alex and I were trying to not be concerned about earlier No, no, that's not the right way firming it. what I think you're missing the point of what Alex's proposing right? He's saying look we can't get rid of sports. Fully there's no world in which we're getting rid of all sports and what he actually maybe know here. Maybe you're exactly doing this. What he's trying to do is expand the scope of protocol changes that we can make without a sport.

**Leo Zhang:** Yeah.

**Leo Zhang:** Yeah, that's why I put it into the last point. I want to existence the cases…

**Alex Hentschel:** How okay.

00:45:00

**Leo Zhang:** because I don't want to explain go to two deeper. I know we are not talking about this one the case we are talking about is there is no State migration, right and there are still a few cases when there's no State migration. There's back.

**Dieter Shirley:** so you go out.

**Alex Hentschel:** Yeah, so there can be State migration for instance, each note could migrate its own local database. it just thought it just not committed as a root hash sort of.

**Leo Zhang:** That's migration.

**Leo Zhang:** I want to differentiate these things. My question is specific execution state where other I call it data base migration,…

**Alex Hentschel:** Yes, yes.

**Alex Hentschel:** Okay.

**Leo Zhang:** right and then migration could be slow. There are three scenes right Backward Compatible. It means there's no probably State database migration and by Backward Compatible. I mean I can upgrades and you can upgrade and the whole network can still work as fine. and there is some fast and slow means you do have a database migration, right? I want to change some keys. I want to compress the database. I want to switch from Badger to Pebble these type of migration takes time.

**Leo Zhang:** when there is this types of four Backward Compatible and fast or even slow. We already have a solution. That is a ruling upgrade. Right since it's Backward Compatible. You can upgrade your node. It takes weeks for you to upgrades it's fine that your migration go offline right on migration. And once you are up you catch up versions you catch up. you can even upgrade but then what cores are not Backward Compatible. what is the experience that we like?

**Leo Zhang:** what's so different from the existing sport when there is no State migration when there is no back work compatible. we could technically just stop at the height and then the consensus note start up first right switch their version First and start building blocks, even though those blocks are not excluded but the whole collection and verification other note who are just waiting for the consensus no to stop building new blocks, and then they will start up and follow up. Would that be the experience that we would kind of achieve and let the not operators to have

**Alex Hentschel:** Pregnant but you go Dido. Sorry.

**Dieter Shirley:** It can I try because I think there's three buckets of network upgrades. And the first bucket you mentioned Leo is the ones where the software is upgraded but no one else needs to know right and performance optimizations are a great example of that and that's where we use rolling updates. Right and it's just sort of like look. I'm somehow internally different as a node, but all of the nodes that haven't changed their software to the version. I'm running don't need to know that right.

**Dieter Shirley:** sometimes there is a change maybe we're adding a field. you could imagine a bft enhancement being rolled out in that way where we're adding a new field that if it exists the new node software nodes to check that and make sure it's correct. The old nodes don't check it and don't produce it. But then the new nodes are our lacks enough to just be like, hey, you're an old note. You're not publishing that so I'm not gonna check it. You're okay. I'll still accept that block and then maybe at some later date we, roll out a new version that does check it right, so that's like

**Dieter Shirley:** Of the bucket two is where there's a new field going out and we're checking it. or we're changing the hashing algorithm that we're using for this thing. And it's not only we all have to agree right and traditionally that's been Cadence code changes, right any sort of cadence feature update behavior update. everybody has to agree when that's happening because if we disagree on which version of cadence we're running then we're gonna disagree on whether or not the execution was done correctly. We have execution Forks Etc, right that's that HCU mechanism and then there's the sport thing where it's like and I guess the easiest way to

**Dieter Shirley:** to qualify why we need Sports is it takes too long? it's too slow for a node to just switch between, a normal delay between one block from the old version of to the new version of software and typically that's been because of execution State format changes where it's like dude we're completely changing the way we're storing the date data in the execution State again, all typically coming from Cadence. And so, we need to take the state that was at the end of the last block. We need to completely rewrite it and then we have to do all that before we start the next block and we

00:50:00

**Dieter Shirley:** we could do that with an hcu, but then the whole network would be like, what would probably fail right or at the very least? Yeah, there'd be lots of problems right? Because if it's gonna take hours, right and so we call that a sport and what Alex is hoping here is that we can take things that conceptually Could be in that second bucket, but today aren't because we don't have a good coordination mechanism, So I don't know. It's just imagine that we change the hash

**Alex Hentschel:** And you feel that A new field in the block header.

**Dieter Shirley:** New Field in the Yeah.

**Alex Hentschel:** That's a very typical thing that comes up. We want to add something like a new hash for Peter's access notes to check additional data, if you just put that in all those will just say I can't you realize your block. That's it.

**Leo Zhang:** Yeah, that's like my point is that maybe we can categorize this different updates and then for different category, we have a way to do it and in your case study talk about It's not Backward Compatible, but it is fast, It's fast.

**Dieter Shirley:** Yes.

**Leo Zhang:** It's just because you can just restart it. All you need is to coordinate at which point you want to restart. Maybe you send a signal to coordinate everyone start at block 1000 will we need to switch version and It's okay. you can upgrades a week later. But as long as you make sure that you will switch version at Height of view 1000 yogurt right but I think do we need to differentiate the two cases where?

**Leo Zhang:** Even though they are both not Backward Compatible but one is slow means you do have some operation when you are offline. You need to stop the note and do some migration and then you start up and during that downtime which this introduce downtime right for the first one. It probably doesn't introduce any downtime, right if there's ten consensus. No you go down upgrades. That's Because there's still nine of them forms of majority continue reading blocks the consensus still okay, but in the slow case, you need to stop at a view and everyone stop at the view and there will be done time. So there is this two different things. I feel like if an both involved involves, there is maybe some not Backward Compatible changes and there is some Backward Compatible changes, but there are some fast.

**Leo Zhang:** But there is no, actions that would cause database migration, but there is some action that causes it we try to different which maybe we just put them into. Different category and so that we bundle all the updates for one category up to update and we don't upgrade at the same time, maybe two of them. For example,…

**Alex Hentschel:** Yes. Yeah exactly.

**Leo Zhang:** if we have three updates for that is Backward Compatible and a fast right? But there is one update that is slow and still Backward Compatible. Maybe we do that one update later and we do three updates that is backward comparable and fast separately that's why I try to kind of make this categorized.

**Alex Hentschel:** completely agree

**Leo Zhang:** and at least a few signals is useful for

**Leo Zhang:** for the not Backward Compatible and fast right does it

**Dieter Shirley:** I think interestingly enough. it's useful for both right I think that this mechanism that Alex is talking about could absolutely be used for a spork as well. And in fact would probably make vishal's life a lot easier if we used it for a sport but because of humans being humans are right if the switch over between the two versions is going to Be more than two minutes or five minutes or whatever number again I don't think there's a hard number right? it's just sort of like the difference between if we implement this right and probably some other mechanisms the difference between HCU and a sport is literally how much down timer we willing to accept before we call it a sport and tell everyone. Hey, you need to tell your customers that your products gonna be down because it's going to take x amount of time for us to do the switch over. because

**Dieter Shirley:** I think the whole goal of this mechanism here. Alex is to say look any protocol change can be an HCU now provided. That the time between the old version running and the new version running is short enough.

00:55:00

**Alex Hentschel:** I would put a caveat on it and that we're able to sort of manage the complexity of this sort of so you were saying we could do an HCU for the whole network? when I think about…

**Dieter Shirley:** Yeah.

**Alex Hentschel:** if HCU they always only think about one node roll. I see Okay, then it's essentially a sport. I think that got your comment.

**Dieter Shirley:** Yeah, am I overstepping when I say hey what if the collection nodes wanted to change the way that collections are formatted right kid. this mechanism? Robust enough for this to be used with minimal downtime and about without a ton of human coordination. or…

**Alex Hentschel:** probably

**Dieter Shirley:** is this because this is view based and the collection nodes are like, I don't know what view it's gonna like. I'm building a collection now, but I don't know what view it's going to be. And so if that collection doesn't get included to what I mean, it maybe Downstream from consensus, right? The verification notes the execution notes definitely but I don't know if the collection notes could necessarily Use this or maybe and maybe I'm going to maybe that's not a discussion we want to have right now.

**Alex Hentschel:** All honesty, I think that again, is one of those things you have those Primitives how much work are you willing to put into putting those Primitives together so it works smoothly or saying hey, this is four weeks of work. Let's just wait for the sport. realistically I think that's a lot where our Traders will be.

**Dieter Shirley:** Yeah.

**Alex Hentschel:** because as you said, they're all little things which create complexity and how we willing to sort of address that complexity on a one by one case basis for each update. we want to roll out one or is that too much work?

**Dieter Shirley:** Yeah, and if it matches a view sorry Epoch boundary, sorry, I'm maybe over fixating on my one example, but because that collection notes basically start a new chain every Epoch, so yeah, we build the old chain using the old block format and we'll build this. New chain using the new block format. And so this mechanism does help provided that the agreed upon view is an Epoch boundary and not just an arbitrary change place. So yeah.

**Alex Hentschel:** That's a good insight.

**Jordan Schalm:** Collection notes also link out to the main chain on a block by block basis so we can do that, too.

**Dieter Shirley:** Jordan

**Alex Hentschel:** Jordan go for

**Dieter Shirley:** you mean link out to the main chain?

**Jordan Schalm:** every block in a cluster references a block on the main chain and they're strictly increasing with respect to the main chains height.

**Alex Hentschel:** It's the same concept of reference blocks for transaction expire. They have to State a reference block and we aggregate that for So collections also right being collector blocks also reference a block on the main chain, which then in terms that it expiry right so you don't have to unpack The Collection you can just say it all the expired.

**Dieter Shirley:** interesting. That's smart.

**Jordan Schalm:** And just quickly. This is not super related to Just something that occurred to me while you were talking earlier During We still reset the view counter back to zero. We should probably stop doing that.

**Jordan Schalm:** because of all these view coordinatives upgrades things that just seems like a Quite bad idea to keep doing that while we're remaining upgrades by View.

**Leo Zhang:** Yeah, we could technically do the same as height right when we generate a new root block. We do height plus one and we just do view plus one as well.

**Alex Hentschel:** Do you still have something Leo you had your hand up earlier?

**Leo Zhang:** Yeah.

**Leo Zhang:** let me yeah, so we are designing a sick away to signal that we have a new version coming up that you can upgrade to I want to mention that for a spork what we do is we wait for the majority to reach consensus that block is finalized and certain block is sealed and then we stop everything right and then we spoke without having to wait for all the notes to reach that height. But if we do height quantity upgrades we like for example a collection now, maybe it's falling behind. Let's say we want to spawn at height 100, but this collection note is somehow just slow and at 95.

01:00:00

**Leo Zhang:** all the consensus note has already stopped and it has a gap from 96 to 100. Right? and this is okay for sport because when we spoke all the node is going to wipe the entire database starting from the new root block, So it already kind of caught up from the root block. However, if we do this High quantity upgrades, We can signal all the consensus notes and maybe the majority of them has switched to the new version from block 100. But what if there's still this consensus note that it was slow at 95 now all the consensus node has upgraded and to a version that is not Backward Compatible. Let's say in the new version and they are starting stop building.

**Leo Zhang:** Blocks from 101 102 but this still one collection node missing blocks from 96 to 100 and seus. No is providing these blocks to them. So do we have a way we might need to think about a way still providing this? old blocks right of previous upgrades to this notes that it was falling behind because we can switch which majority but all the rest of the notes still have to catch up the missing blocks I assume if there's an upgrades that is not Backward Compatible when you upgrade you no longer be able to provide blocks for the previous version from 95 to 100 and then

**Alex Hentschel:**

**Dieter Shirley:** But isn't even worse than that? let's say we say I'll removing to a new block format at view 100. There might not be any blocks in views 95 through 99, right? So

**Dieter Shirley:** I think when do I turn off right I've seen a block with you 95 and I'm looking at that block and I'm like, okay, there was a block with you 95 there could be up to four more blocks and then a new block comes in and it's a format. I don't understand but how do I know? That we're actually a view 100. And I should switch over.

**Alex Hentschel:** I think that's exactly the questions. We would need to solve on a Case by case basis again, this framework doesn't help It only says it now it's time. I guess you don't know what you do. I guess you're screwed here.

**Dieter Shirley:** but is that case by case or is that just a problem that all non-consensus notes are going to have

**Jordan Schalm:** I feel like you should try to not make the block model backwards incompatible. right because in most cases, I don't think that would be the case that it is. Most of the time even though you might not understand that's kind of the mental model we have for the protocol State even though you might not understand what's underneath the protocol stage key Value Store. You should still understand it wrapper the block. which

**Dieter Shirley:** so block format changes would just always have to be a sport. Is that more or less the statement?

**Jordan Schalm:** Or not necessarily a sport, but I don't know you can imagine for these kinds of edge cases where you're changing something Really deep and important to do it in kind of a two-step fashion refers to roll out something that allows you to understand both potential formats. And then you do the final upgrades. I don't know.

**Jordan Schalm:** hopefully most things aren't quite as breaking as that example.

**Alex Hentschel:** The block format is particularly tricky because consensus notes scan the past history, so let's assume they're now at the new block format open up the database, pull out the old blocks because they want to say if the new block they're getting has any duplicated transaction. Sorry collections in it compared to the last 600 blocks, they still need to understand the old block form. and all we have to migrate the database which is also I guess that that's all the issues were we're sort of running into when we try to think about this as a what would we need to do to help all those problems and I think our best answer now is let's just see where we get with this right and what we need in additional tooling.

**Dieter Shirley:** Yeah.

**Leo Zhang:** So basically we try to make it as much Backward Compatible as possible, even though we are changing. Let's say block hashes, but we would say below block 100. We will use the old way right and up to above 100 has using that way we won't have that issue for slow notes to catch up.

01:05:00

**Alex Hentschel:** Yeah, Yeah, that would be an option, and I think again that's largely a case by case basis.

**Alex Hentschel:** So I mean honestly for me in this discussion already has really helped a lot and to validate that we're not complete these sort of overlooking some aspects here. We have 20 minutes left. I'm not quite sure what the next steps would be, is one option could be that we've talked about it. Where I guess The Primitives that the dynamic protocol stage will provide as of Crescendo launch. I good enough. We're just going to experiment with it. Do we want to continue this discussion? Maybe use one or two?

**Alex Hentschel:** Example cases of upgrades we used or we had to kind of go through and see what we would need to do. I don't know. what's your feeling as this is officially a protocol stop working group here. Yeah. Peter

**Peter Argue:** Who's our personal? Okay.

**Dieter Shirley:** but

**Peter Argue:** I think it would be helpful to put this into the context of existing use cases. So we've got hcu's for execution verification notes. There's some I wouldn't call them bugs but gaps in functionality that I think this clearly could clean these off and then access nodes as well and the coordination around the Cadence version or the fem version that they're able to support with their current software versions. And so I think those are three use cases that we have immediately and it would be useful to look at how this would apply to that.

**Peter Argue:** Maybe not necessarily on this meeting but as a first

**Alex Hentschel:** Yeah. I'm totally on board. The only flag I want to say is that at least for the other notes? for eons and VNS. We have a mechanism for contentious notes, right? We don't even have anything So I'm wondering if it would make sense fast strategically to refine what we already have or maybe sort of start looking at in for other nodes where we don't have anything yet.

**Peter Argue:** Kind of to eat's point do we have something we wanted to deploy in a non-spark fashion or those notes now? Because certainly have stuff for verification and…

**Alex Hentschel:** is Yeah,…

**Peter Argue:** execution notes.

**Alex Hentschel:** I assume that something like a block Had A Change a new field would probably be something that will come up within the next 12 months.

**Peter Argue:** Okay, so based on our roadmap. You think that that's something that we're going to run into?

**Alex Hentschel:** Yeah, at least over the last years we usually added fields or modified the structure of the Block in Minor Details, the last thing I'm thinking about is that extra hash we edit for the change register so that the AI and stone have to download the entire try. they can just wait download the register changes from the execution notes and rebuild their state. Yeah, But I don't know,…

**Peter Argue:** look

**Peter Argue:** That's fair.

**Alex Hentschel:** .

**Peter Argue:** I mean, I think at the very least we should use cases to help inform the initial designs because there's something that we know we're gonna have to do.

**Alex Hentschel:** Okay. Vishal

**Vishal Changrani:** Kind of on the similar lines I think what will help is having a long list of table which kind of just list out all the types of upgrades and whether or not We can use this approach for those upgrades and avoid a sport. So for example parents changes to blockhead execution State migration which obviously is a huge long list that will also kind of help Show value for this whole feature. Basically if you can say okay, these are 70% of upgrades that have happened in the past. Would have been done without a sport if you had this feature.

**Alex Hentschel:** I have mixed feelings. I certainly see the value of such a list from a product perspective. the problem is that I think sort of conceptual feasibility is a very impractical measure, a lot of things might be tractable or sible. engineering expensive that in the end will still say we're not going to do it.

01:10:00

**Alex Hentschel:** I'd say we're waiting for the next book.

**Dieter Shirley:** yeah, I'm a little nervous about what you suggested as well Vishal because it's sort of like if I could snap my fingers and have that sure but that's all that that is a lot of work and at the end of the day there is no upgrades that used to be a sport that could turn into an hcu. That wouldn't use this mechanism. You know what I mean? it's like and so long as we can think of one or two plausible examples that are likely to happen over the next year. This is not such a complicated mechanism that we're like, man what a waste of time. It was to build this I don't think anybody here is going we'll never use this right or I can't imagine. Yeah, I give it 50/50 that over the next year there's a hundred percent chance that we will use this.

**Dieter Shirley:** And it will make an HCU possible. That wouldn't have been an hcu. Otherwise, it would have been a sport right now. Is that going to be 10 times or is it going to be three times? Is that going to be giant things that are massive unlocks for the protocol that if we had waited for the sport to do it. It would have been like a disaster and a big Market misleading Thing versus it's better like protocols better. We're all happier, but hardly anyone noticed certainly not the business people.

**Dieter Shirley:** I don't know but it's inconceivable to me that this is not useful and valuable in the next 12 months to release software that at least we care about and more easily and then what we would have done in the past and it doesn't seem like it's a huge lift. And so to me it's kind of a no brainer and I almost feel like arguing for it more strenuously than what I just did in the last two minutes is not necessarily a good use of time.

**Vishal Changrani:** I guess.

**Alex Hentschel:** Do you want to respond to that Vishal?

**Alex Hentschel:** Yeah, sorry, go ahead.

**Vishal Changrani:** Yes, one quick response.

**Vishal Changrani:** Finally, if you don't like we can attempt to compose that list I volunteer to try and compose that list and see how far I can get but if we can confidently just say that with this mechanism we at least avoided one additional sport. I think that's more value than anyone could ask for after this mechanical place,…

**Dieter Shirley:** What?

**Vishal Changrani:** if you could just say that confidently then that's

**Dieter Shirley:** the problem is that I don't think that's The right metric is that we'll have at least one software release. That won't have to wait for a sport that in the past would have had to wait for a sport and you could say we're gonna have one less work. no, it might be a thing that we would have never done a spork for which nonetheless is valuable if we can release it without a sport, know what I mean? and I'll just use a performance update because I don't know that this will be the case. But imagine we had a performance update they made the network run 10% faster or even twice as fast right? We're not overloaded right now. The Network's not overloaded right now. We would never have a sport to speed up the network right now today, but being able to go and run benchmarks and say look our networks twice as fast today was yesterday that has value it doesn't have enough value like you can't say we avoided a sport but you can say that we ship software right? and I think that's the real metric that we're gonna hit.

**Dieter Shirley:** This is that we will be able to ship earlier and more often and rather than we'll have fewer sports. Right? I guess if that makes sense.

**Vishal Changrani:** It is.

**Alex Hentschel:** Thank you, Dieter. Yes. Yes exactly.

**Dieter Shirley:** it's really Bonkers to me. Sorry, I'll just finish this thought Jordan. It's really Bonkers to me that I spent the first half of my career doing software releases before I got into continuous deployment. But I think most of you have spent your entire career doing continuous deployment more or less and the fact that we can't do that on this project is it's killer right and this is a step towards that

**Jordan Schalm:** Yeah. I just wanted to provide maybe a different framing for this feature which might be useful in the context of that list and everything the feature that we're building right now is we're moving a whole bunch of the protocol State into this key Value Store thing, which is committed to and a hash and every block. and we're creating a mechanism to upgrades two very specific things the data model of that key value store and the state machine which takes the last Q Value store and turns it into. The next key Value Store instance based on The View and the blockchain and not the black eye, but whatever you want. Just a state machine that says here's the next blocks vertical stand.

01:15:00

**Jordan Schalm:** in some sense. That's the entire feature. That's where we're making. It happens to be true that we can sort of overload that scene mechanism to upgrade other things.

**Jordan Schalm:** but upgrading other things is like what Alex was saying? It's totally on a case-by-case basis and it's not totally clear to what when and where and and how you would make make some work very every different case. But even independent of that you still have this ability to upgrade.

**Vishal Changrani:** Jordan can I say that with this new feature of the key value being on chain isn't like the score also now more decentralized where nodes have to form a consensus at least the consensus notes. To kind of decide on whether or not an upgrades will happen. Let's say two-thirds of the nodes don't decide then. The spork in a way will not have today where the sport will always.

**Alex Hentschel:** No, I am that would be when we add that extra thing Dieter described upfront, we don't activate the new software version unless enough notes are sort of on the new version already. Right what the current thing does it says then the new protocol is hitting you're not updated you're down, it will just run it and crash group.

**Vishal Changrani:** But it's an on-chain thing, So it went through the regular protocol consensus, right?

**Alex Hentschel:** no, no, it's a No,…

**Jordan Schalm:** it's a

**Dieter Shirley:** It isn't Alex.

**Alex Hentschel:** it's essentially just a governance mandate put in code the governance, as governance people say then it's a new software that you resend the governance transaction that goes through service event arrives at the protocols. There is not a Pro cost States has the human set view 10,000 that's going to be it.

**Dieter Shirley:** Right, but it still happening through the protocol in a way that consensus nodes can't veto but they have confirmed and is publicly visible right in a way that Vishal calling up a note Opera here and say okay we're going to update this, tomorrow there's a meaningful difference even if to your point, they don't have veto power right like you're saying hey, no, no, it's not consensus in the sense that they could choose otherwise, right but it is consensus in the sense that the decision has to go through the smart contract has to be, confirmed as correct by the consensus nodes, even though it is not the case that the consensus node can follow the protocol and not include that right.

**Alex Hentschel:** Yes, I think that is a very good argument. And in this sort of they have to look at it and validate it we can do safety checks. hey, you can't just upgrades the protocol in 10 views. That was a human error. We're not doing that or you can't downgrade it to a lower version. No also not so that will also give us a lot of sort of ability to catch human errors right in this process at least.

**Dieter Shirley:** and it can't be done without the multisig.

**Alex Hentschel:** If you run it through yes. Yeah.

**Leo Zhang:** So let me confirm my understanding one more time. So basically we Implement a state machine in a software and the state transition will only triggered by those transactions signed through those typical transactions by operators and operators themselves cannot trigger State transition by simply upgrades their software because they can only change the state machine. The state machine can only be triggered by the transactions, Carrying the signals to trigger the state transition.

**Alex Hentschel:** Yes.

**Alex Hentschel:** Yes, essentially what the logic that we have implemented or are implementing right now is it listens to Service events? that's the input Service events. So anything which came through from the execution environment has undergone verification and feeling that is being picked up and whatever, that gives us a very very general message bus, from the execution environment to essentially the running Network. Which we didn't have before and we can use that to coordinate upgrades we can use that to set parameters we can use that for a whole bunch of stuff. We already using it for the epox which over right it's also information coming from the execution violent going to the protocol.

01:20:00

**Leo Zhang:** Yeah, and then Why do you design a key Value Store instead of a version? For example, right let's say version 2 from version. Let's say we are running on version 1 okay, the next version two is going to upgrade. The header ID how you calculate or upgrade header? So what do you suggest is that?

**Leo Zhang:** The Operators or whoever will need to sign transactions and send it to the system. contract to trigger

**Jordan Schalm:** the governance committee not operators.

**Leo Zhang:** Yeah, yeah The system event will Say something that the hash function will change from A to B or what you say the version will change from one to two and the changes in two is actually the word changing the hash function. so what…

**Alex Hentschel:** the letter

**Leo Zhang:** if the latter But then why do we need the key values? We could just use a version? right and…

**Alex Hentschel:** Yes. We could I think it's helpful to remember…

**Leo Zhang:** let's say

**Alex Hentschel:** where it came from the epoch transition. So, where we also want to associate with blocks as of this block. Alice will join at the next Epoch, that stayed up, and then we realized for EFM record or epoc fallback mode recovery. We want to store more State information related to each block, right and then we're like, we can use that for version upgrades. I see it's yet just another field in our key value store. Right? What you just said is why don't you store the version and we're exactly just add a field to the key value store. Right which has execution notes version is now this, and then from there on you can use that to trigger version upgrades.

**Dieter Shirley:** What and…

**Leo Zhang:** right

**Dieter Shirley:** I would potentially go the other way and say maybe we shouldn't have a single version number for the protocol. Maybe we have.

**Alex Hentschel:** Absolutely. Yes. Yes.

**Dieter Shirley:** Right, Cadence is a great example, we'll use an HCU to upgrade Cadence. And now that Cadence runtime is version 72 and starting a block, whatever turns out we fixed a bug where when you add two really weird numbers, the least significant bit is wrong.

**Dieter Shirley:** And we're fixing that bug, but guess what? if you mix those two versions you might end up with a mismatch right where the flowing point is different in the very last number and no one noticed but now it bitwise those are two different results. And so we have to switch Cadence over we could say we're going to a new protocol version and the only difference between protocol version 112 and 113 is that we're moving from Cadence 72 to Kaden 73, or we can have a separate field in this key value store. That is the Cadence version which might actually be easier for humans to deal with because now as humans, we don't have to go to a web page that says the difference between protocol version 112 and 113 is X Y and Z we can just look at this protocol State and the thing that changed that at view height, whatever is that the Cadence version went from this to that so

**Dieter Shirley:** I'm not saying we have to use it in this way or that way, but now that you bring it up Leo. I think there's an arguement to be made that there's a bunch of stuff that we might hide behind. in protocol version, whatever The View back. What is it? The reference block height is X far away and now we've moved to this version. And so now the reference block is this far away. Maybe that's just a field in that protocols state that is literally just at such and such a height. Now the view the look back is this mini blocks instead of that many blocks. and so it actually I think makes it a lot easier and more explicit as to what's changing instead of just this opaque version number went from X to Y and then you have to go and look up somewhere what that means.

**Alex Hentschel:** Yeah, and in fact Peter, our implementation already assumes that they're going to be very many versions because what we're currently versioning is literally only the key Value Store it tells the key value started tells can say I can do breaking changes and I might require reboot. Right? And the breaking change could just be all we're adding the update functionality for yet another node, right? So That's why we call it The minimum possible sort of thing to even do some upgrades.

01:25:00

**Alex Hentschel:** very nice. Thank Where time can I ask do we want to continue this discussion or so? I have on my list that we wanted to do two examples as my suggestion would be that we do those examples after we've shipped Crescendo. I don't want to distract the engineers was yet more work, Yeah, but if you wanted to have this thought of this cartoon more on how do we want to proceed earlier? I'm happy to

**Dieter Shirley:** So let me summarize what this meeting was for right?

**Alex Hentschel:** thoughts. Yes.

**Dieter Shirley:** Y'all created a mechanism. And you weren't sure how useful that mechanism wasn't going to be in a general case, but it was pretty clear. He was going to be Somewhat useful but not all the ways that we could use it. We've also talked about a bunch periphery stuff that influences are thinking about this.

**Alex Hentschel:** get

**Dieter Shirley:** But my current feeling is that this mechanism it exists, which is awesome. I don't think you guys are doing any extra work to expose this. All right.

**Alex Hentschel:** a little bit but yeah, let's be a three weeks. I think that's totally fine.

**Dieter Shirley:** okay, so more or less we've committed to this mechanism even it's not entirely built yet and…

**Alex Hentschel:** Yes.

**Dieter Shirley:** and I am still firmly of the belief that this mechanism. it doesn't solve all of our problems solves enough problems that I'm really excited about it, and I'm glad that we have this stuff and

**Dieter Shirley:** we all learned a lot but none of this stuff. I think what we learned or what we discussed none of it rises to the level of hey, we need to change this mechanism Right and so I'm really comfortable saying yes, this is good. Let's ship this let's start talking to teams when they want to push software updates. Let's ask them how they want to use this mechanism. Do they need to use this mechanism. How do they want to use this mechanism and I agree with I think the statement you've made multiple times Alex is that which is let's not decorate this mechanism anymore in an attempt to make it more useful for the general case until we've gone through more specific cases and start to see patterns of people keep making the mistake of not giving enough lead time. and so let's put a guard on this where we have enough lead time or

**Dieter Shirley:** People keep using it for something that actually should be just a rolling upgrades. So let's write some documentation around not using this when you're the ruling upgrades or if vice versa right people keep doing rolling upgrades and then putting in weird logic where they're trying to detect what the other node is doing and instead let's just tell them to use this instead. So I like that I think this is General enough to be useful in a bunch of different scenarios. And before we start trying to make it. More complicated and maybe more useful in various scenarios. We should see those scenarios play out.

**Alex Hentschel:** Amazing summary deed if you want to use it come talk to us Jordan Yuri and myself. We're gonna help you make this work, So it's not that you just have to do it, and I'm also super excited about seeing the ship. Thank you. This was an amazing meeting and hope to talk to you soon.

**Dieter Shirley:** things everyone

**Peter Argue:** Thanks guys. Thanks Alex.

Meeting ended after 01:29:10 👋

