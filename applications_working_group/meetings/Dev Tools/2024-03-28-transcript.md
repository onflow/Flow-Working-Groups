Dev Tools Working Group 
Thu, Mar 28, 2024

0:00 - Tom Haile 
cool hey geo let's open a couple of guys show up to give some status on the tools and stuff that they were working on I think that Hopefully you can give a little status on the flicks. I'll put flicks status in the agenda. So I think it'll be kind of interesting to talk about just the approach of on-chain, you know, with the flicks as a priority kind of post the Crescendo update. So just give us a little bit of background. Give us a little teaser. That'd be fun. And then she'll give us an idea of the bridge and the EVM cadence integration. That'll be fun. The audio is not going to make it today. And hopefully a couple other guys will show up. But we can kind of kick this off. From the agenda perspective. Not a whole lot to say about OKRs and all that. Basically, we have two main focuses for the foreseeable spread, or what we call the cycle, is the Crescendo upgrade, which will consist of, you know, WKDNs, KDNs 1.0, and EVM compatibility. You know, so we should all know about this. We've been talking about it for for a while and then the king's window migration status the interesting thing coming up is actually doing the migration. So testing migrations and that should be kicked off, I think, first week of April. So next week, sometime in the next week, hopefully. Yeah, I'll have more information on that. And he's available on the Thursdays, which is today, community dev meetup thing. So usually, but I think he's been out on on a vacation or something. And so that's kind of the migration status. The contract migration tools, just wanted to get some input from anybody. They're finding any of the tools that are available now, like the linter, and, you know, just the tools that are available in VS Code with the Kains 1.0 versions. If there's any issues there or anything that needs to be addressed, you know, kind of open the floor if anybody wants to say anything. If if not, then we can we can have geo you've kind of a status of the medium pins bridge integration stuff And anybody can speak up at any time if you have anything Yeah, I haven't had a chance really

2:57 - Giovanni Sanchez 
to use too much of the migration tools. I've used the CLI to stage and unstage and do all of that. But the step beyond that, emulating the migration, I haven't had a chance to play around with. I think Naveed, who's not here, and Sukuna have been working together on making sure that that works well. But yeah, I guess I'm happy to take it into a status update for the bridge, if no one else has anything else.

3:26 - Tom Haile 
Yeah, yeah, I just think this meeting kind of being short a lot of the guys have been out over the past couple of weeks so there hasn't been a lot of progress in the tools arena and The real the real kind of work is being done on the protocol side and Anyway, so yeah. Yeah. Good. You know, I appreciate it No worries.

3:48 - Giovanni Sanchez 
So I had a couple PRs stacked from like proof of concept through kind of like a simplification. So those went through review, seemed like we had pretty good alignment on that. So those are merged in main. What's on main currently largely reflects like the general call flows for like a For NFTs, it'll be similar patterns if you do end up taking a look at that for bridging fungible tokens. Progress started on that yesterday, and that is pitching in. And we're also starting to build out some tests. We're getting some help from, I guess this is also relevant to tools, from Peter, who's been like a really the main, like a primary contributor to the Cadence testing framework. So he's taking that as an opportunity to help out, which is really appreciated, and also look for opportunities to kind of like build out additional feature sets into the testing framework. And I guess with respect to EVM, just make sure that there's the features that are required to build sufficient tests between Cadence and an EVM contract integration. So that's really helpful. That will build in some tests, and I'm hoping there won't be any major security findings through that process. But that will be helpful to uncover anything that might be not just not working for the happy path, but also add in some defensive tests as well just to validate that everything's working as it should. From there, I guess my plan really today is to continue to pick up the fungible token path so we can get bridging and the timeline that I'm shooting for. Was originally April 15th to get that to a place where things are stable to get a stop on code progress for auditing. It's looking like it still remains pretty likely, although maybe another week of buffer just for some things that are going on personally for me with that kind of introduce some uncertainty around that timeline. But pretty much mid to third week of April seems to be where we should be at a place where we have something that we can probably just deploy to PreviewNet. And between getting an audit and having real world use, hopefully on PreviewNet will result in some feedback that will be really valuable for uncovering anything that needs to be either added in or patched up. So yeah, if you all do have a chance to take a look at the code for the bridge, I'll be updating the flip, updated the interfaces for the flip yesterday. And I need to update some of the diagrams and the content of that flip to reflect what's actually merged the main for the flow EVM bridge. But if you all do get a chance to look at that, I'm also happy to cover it at a later time, a little bit more in depth, because there's quite a bit of code to wire everything together. Nice.

6:56 - Tom Haile 
Much appreciated. What would you say the breakdown is of solidity and cadence in the whole bridge? Yeah, that's a good question.

7:08 - Giovanni Sanchez 
It's mostly cadence. It's virtually all cadence. There's a factory contract in EVM. And then there's templated ERC721, and I guess will be ERC20. But all of the orchestration, all of the requests, all of the routing for all that stuff is all happening in cadence. So it's large majority cadence code That makes sense.

7:40 - Tom Haile 
Am I correct in saying that all transactions go through the cadence sign? Yeah, yeah, exactly.

7:46 - Giovanni Sanchez 
So bridging to EDM, I guess. Yeah, so that's it's a The bridging functionality has been integrated into the COA, so you'll be able to just call into your COA, deposit an NFT, and it'll just pop on the other side to an ERC-721 that corresponds to the KNX NFT that you gave. It'll be largely the same for fungible tokens. But there's also like an actual interface with like static global methods on the bridge contract that you'll be able to call. So you could, you know, give an NFT to the bridge when you call and then name another recipient, like any EVM address you'd be able to bridge to. Oh, nice.

8:33 - Tom Haile 
I'm super curious about randomness on the EVM side. Would the bridge be able to offer that or would it have to be kind of baked in through more of a protocol level side?

8:49 - Giovanni Sanchez 
Yeah, so we could definitely inject randomness. It doesn't have to exist through the bridge. The bridge leverages like contracts that are available to anyone, really aside from the integration with the EVM contract. But the bridge itself really leverages the COA and that interface to call into EVM. So really, technically, it's not anything stopping from anyone else creating their own bridge. But yeah, so the randomness. I have a proof of concept for like a lottery, like a solidity lottery contract where you can inject randomness from the cadence side. But I think the ideal case would be it's accessible. Like you could call a method from solidity and access randomness from the EVM side directly. I don't know what the plans are for that, but that's kind of like my ideal case. But maybe there's a way that we can create either a pattern or a pattern for injecting randomness from cadence into EVM. Nice, nice.

10:03 - Tom Haile 
So generally speaking, would the pattern be write cadence to offer functionality and then expose it to the EVM side, and then essentially leverage features in cadence on the EVM side?

10:22 - Giovanni Sanchez 
Yeah, I guess in the case where it's like available in the cadence runtime and not available in EVM, like randomness, then that, yeah, that would probably be the pattern. I mean, there's a, the way that I did this is like a little bit more of an advanced kind of, I'm having trouble finding the repo right now. But yeah, so it was like, you have a solidity contract and the owner can inject a random number, but the owner of the Solidity contract is actually a COA inside of a Cadence contract. So you're wrapping the call to inject that randomness in Cadence smart contract logic, and you're not trusting some random person or off-chain Oracle to give that random number.

11:13 - Unidentified Speaker 
Right.

11:15 - Tom Haile 
Thanks, Ari, for recording. We do have the AI bot going. All right, very, very interesting. Yeah, very interesting. Thanks, Joe, appreciate that. Any questions for Gio on any EVM cadence integration? I think more is like helper contracts and contracts in general as tools to aid in the development process. Anybody have any questions?

11:50 - Akos Erdos 
I would have one question, actually. Is it correct there is an RLP encoding functionality on the EVM side that we could leverage on Kden's side as well?

12:07 - Giovanni Sanchez 
Well, I guess you said RLP encoding functionality from EVM?

12:14 - Akos Erdos 
Yes.

12:16 - Giovanni Sanchez 
I'm not sure if that is... Something that, because I guess just generally like the direction between like state change and the ability to kind of like inspect between VMs is largely cadence to EVM. So from EVM, you're not able to like inject from EVM to cadence. It's going to only occur directionally from cadence to EVM. But there's, I guess, maybe the possibility of like there's ABI encode decode built into the, to, into the EVM Cadence contract, which is the interface for access between Cadence and EVM. If that's a desired feature that would be helpful, then maybe it's worth creating an issue or chiming in on the Flow EVM Discord channel, asking if that would be a possible feature to implement in Cadence.

13:08 - Akos Erdos 
Actually, the reason I'm asking it is in cadence, there is already decoding as part of the language, but not encoding. And when I was trying to figure out how, because my use case, what I'm building, I will need encoding. For it. So I was looking around and somebody suggested that I could use the RRP encoding that is there on EVM. So I need it from cadence direction. Um, okay, let me think about that.

13:51 - Giovanni Sanchez 
Is it, uh, I apologize. I'm not super familiar with the, with that functionality. Is that like a function call that you have, uh, when EBM like within solidity?

14:04 - Akos Erdos 
That was, so the suggestion was, I guess, just mainly just to work around the fact that there is no encoding in the cadence language. So, but there is potentially something I could leverage that is already there in the EVM side. So, I can just call the EVM, I'll make my cadence smart contract to do the encoding of the information I need to encode and then get it back and work from there. Yeah, actually, that approach does make sense.

14:44 - Giovanni Sanchez 
So if you have a util method on a Solidity contract, you can call. It's like RLP encode. Then from cadence, from a COA, you can call into that contract. And then I'm assuming you get back bytes, like a byte array, or do you get back a string?

15:05 - Akos Erdos 
Yeah, it would be a string, yeah. Okay, thank you.

15:10 - Giovanni Sanchez 
Yeah, that would be an approach that you could take. Okay, cool, thanks.

15:18 - Unidentified Speaker 
Nice.

15:20 - Tom Haile 
Yeah, bi-directional would be very interesting, as you say. Because I'd say both environments have function to offer each other. Cool. Well, Akos, since you're warmed up, can you give us a little blurb about on-chain flicks and where that effort is? Okay.

15:49 - Akos Erdos 
Yeah, I didn't really prepare to talk about it, but yeah, definitely. Yeah, just a summary.

15:55 - Tom Haile 
No charts or anything you need.

15:59 - Akos Erdos 
So we did have the Flix working group separated from the Tools working group previously. I was interested in the Flix from the security perspective of blockchain transactions, so I joined the working group. Flix is about storing metadata and other information about transactions. And basically make it available to consumers and provide information via this mechanism to users so they can get information. Okay, what is the transaction doing? Is it safe? Is it audited? And then many other stuff. So that's Flix about. That's already existing. I assume you all know better than me what it is. So we discussed, okay, we have Flix templates already, but what is the better way of distributing these Flix templates? There are currently the flix.flow. Qom has a, that provides REST APIs and I believe ML City has another, so they are operating another version of this backend that gives you the flexes. Or you can look up on GitHub accounts, like where somebody puts their flex templates out and whatever other ways. So, but this way we found it would be better if there is a way where when someone want to publish or introduce a new transaction and the transaction template or interaction template, so they can do it in a centralized way, so they don't have to go to flow foundations or MNLCT to expose these templates, but they would get a really decentralized way of approaching this. So we made a decision that we're going to store the templates, interaction templates, on an on-chain registry. Basically, that would enable anybody to have their own version of the registry, which is actually a resource that would be on those accounts who want to operate the registry like that. And basically, that's the main thing we started to work on as part of this Flix working group. There are a lot of toolings that would be utilizing these on-chain Flixes, so we discussed that the Flixkit and the Flow CLI would interact with the on-chain Flixs. We also discussed that, well, it's not 100% related, but okay, so let me walk through the chain of information. So the course for Flow that Brian is building, so he would use also the on-chain Flix is a single source of troop and he would expose it with his system via his REST APIs, which would potentially be the flix.flow.com in the future. So, we also discussed that these APIs could be consumed by tools like Kotlin Browser, or if PRT has an appetite for that, then do it in ProTiger. Or whatever other ways of consuming these APIs and making these interaction templates available for everyone, for the developers and the users. The Flix, so the... Flow.flix.com API is already integrated with the flow reference wallet. I just am always thinking about Liliko flow reference wallet. So basically by swapping out the internals, that functionality will still remain. What else I can talk about this?

20:55 - Tom Haile 
Yeah, yeah, yeah, I appreciate you went you You went a bit more in detail than I that I just but I appreciate I appreciate that. Yeah, the the Interesting thing is so Icos is in charge of the on-chain blips kind of integration the the one thing that I find interesting is that Flix has gone over a couple of versions. And so how do you, how does one know which is the current version? That kind of thing, because Flix kind of sit by itself in a JSON format. So JSON format is just one format of the Flix. Having everything on chain and then having users be able to update versions and deprecating older versions and always having a pointer to the newest version, essentially like a DNS, like a domain name, somewhat, then it gives the consumers more of a confidence that they're using the latest and greatest, you know, that kind of thing. And as Echos mentioned, Brian is working on a digestion service, aggregation service, that will make all that stuff available a lot faster than like wallets and stuff like that, looking at a punching. But it can always be looked at punching. But yeah, yeah, appreciate it. Appreciate it, Echos. Thank you very much. Any questions from the community about Flix? No, okay, good, good, good. Kind of the last thing is any community tools, any community tools updates or anybody see anything that they found interesting in the community tools that they wanted to highlight? Hey, Pace. Hey, oh, yes, Jeff.

22:56 - Giovanni Sanchez 
Yeah, I haven't gotten a chance to use it, but I think between the last meeting and on this one, there was something that came out from Flowser. I'm not sure how to say it. But I'm wondering if there are any stated plans for that to play a more central role. Yeah, especially in the context of Flix, because I could see Flix becoming a bit of like a slider UI to interact with contracts. And Flows being a dev tool would be a good place for it.

23:36 - Tom Haile 
Yeah, that's a good shout out. Yeah, definitely. The ability to auto-generate UIs, like a Swagger, or a Postman was another one, in order to leverage Flix does make sense. The idea was to have that in the contract browser, or in Bartha's tool, I just based on it. What's the Back Explorer that we're talking about? Anyone?

24:10 - Unidentified Speaker 
Anyone?

24:15 - Tom Haile 
In order to kind of add the functionality that ether scan gives are on the side. So, looks gives that ability as well. To describe all the inputs and all that kind of stuff and call contracts with a pretty complex transaction or script. I'd have to look into Flowser and see what kind of integration points there would be. But yeah, it's a good call out.

24:48 - Giovanni Sanchez 
I mean, while we're talking about Flix, one of the things that came up, I was talking to some folks at eThunder, actually the folks who worked on Flu and Flux, And one of the main pain points was not having type safety between calls to cadence scripts and transactions. And I think that's something that they built into the Flux tool. But I was wondering if there's a way that we could wrap Flix so that you would have that similar type of type safety in either FCL or downstream.

25:24 - Tom Haile 
So we have that in generating TypeScript wrappers for Flix. Well, it's a TypeScript wrapper for FCL to run Flix. So we have that. And it gives you your type safety as much as TypeScript does. There's goals in the future to expand the language support from JavaScript, TypeScript to Go, Go's logical next step. And so, yes, type safety would be super awesome. I totally agree with that.

26:03 - Giovanni Sanchez 
If no one has anything else, I also have, I guess, a feature that I built into the bridge, but that might be helpful for more context than just the bridge. It's like NFT serialization. Yes, I was going to ask about that. Yeah, I have a PR app for it for the bridge. And I use it basically to bridge metadata from Cadence into EVM. But I have... The stuff that's on the bridge is all Cadence 1.0. So there's this script that I have. Let me make sure that I actually am sharing. Oh, shoot. I might need to just kind of screen share if I'm going to show it here because it's sharing right now. All right. Are y'all able to see that? Yes, you can blow it up a little bit. Is you see it's just kind of this main entry point for a script. Three parameters. I take the collection address, the storage path identifier, and the ID of the NFT that I want to serialize. This is running on mainnet right now. And then basically, I just took the stuff that's currently in the serialization util and put it into this giant script rather than deploy a contract. So right now, I have an address for my account on the Doodle Studio. And an ID. I figured I would use the doodles, because doodles have a whole bunch of nested NFTs that you would want to represent in serialized metadata. When I run this, I should get back a data URL. And that data URL, if I just go over to, like, prettify JSON. Great. Click on my first link. And I'll go up here and remove Just like data URL, we can kind of take a look at what this JSON looks like, Make pretty. So now this ad gets out of my way. You can see this is all in like open seas metadata format. You have the name, description, image, external URL, and then all these attributes are actually coming from nested NFTs. And so you can imagine that like in the context of a bridge, you'd have some NFT that's bridging from flow from cadence to EVM. And you're taking all of those, those metadata views and serializing them into the format so that when you commit this value as a data coded URL, as a data URL to the token URI in EVM, you would get that in a format that like OpenSea would be able to render it. So, and then question is.

29:08 - Tom Haile 
Uh, any support for, since there are owning other and all that kind of stuff.

29:17 - Giovanni Sanchez 
Um, that wasn't slated for like the first, uh, round just because I guess it just felt simpler to go from one to one. The other, the other, and maybe this is like a misunderstanding on my part, um, is 1155 allows for you to define like an ERC 20 and an ERC seven 21. So there's the possibility of like mixed types of assets in 1155 I kind of just wanted to avoid. Um, is that, is that true?

29:47 - Tom Haile 
I, in my, in my experience, 11 to 50 fives can own ERC twenties and, uh, uh, seven, 20 months. Am I saying that right? Seven, 20 seven, 50 months. Anyway. Uh, yeah.

30:03 - Unidentified Speaker 
Uh, seven, 21.

30:04 - Tom Haile 
And yeah, I love, uh, and 11 55 is give you the ability to have like a semi fungible, uh, asset.

30:15 - Giovanni Sanchez 
I see. Yeah, especially that semi-fungible makes me a little cautious, because we don't really have an analogous standard and cadence for that. So we kept it to just 721 and ERC20. But I'm sure there's something that we could do in the future to incorporate that, because especially the main bridge contract doesn't really have any fields. There's additional. Like config and util contracts where that status out. So should be pretty extensible.

30:50 - Tom Haile 
Okay, cool, cool, cool. Yeah. And OpenSea handles all these energy standards and stuff. So probably just conforming to whatever their standard is, you might get it all for free. That kind of thing.

31:02 - Giovanni Sanchez 
Yeah. So version two.

31:14 - Tom Haile 
And we got a demo. That's cool. Anything else on EVM Cadence integration? Questions for Geo? All right, cool, cool. Any particular updates you want to give about the Dependency Manager or any FCL changes?

31:43 - Chase Fleming 
goals in general. I was out last week but um so although I did just finish the uh the requested feature about the dependency manager where if you're adding it if you could um automatically add them to your deployments accounts so once that's merged um and released would be usable so basically if you're going to say like you spend and adds them. If it's not a core contract, it'll interactively prompt you to select from the accounts that you have which one you want to add to the emulator deployments. So it just speeds up that process for you.

32:28 - Tom Haile 
Nice. I guess I have a question. Maybe we know the answer. Working a black chain. So does the flow CLI make it easy to fork like test net or main net to your local emulator or anything of that nature?

32:48 - Chase Fleming 
Uh, you mean like locally to like simulate something or what are you? Yeah.

32:53 - Unidentified Speaker 
Yeah.

32:54 - Tom Haile 
It's like, Hey, I want it. Yeah.

32:57 - Chase Fleming 
Yeah. It's been on my list for awhile too. Uh, write docs up for that. Because I think that's a feature we have that was never written. So I know Greg's on here. I can add that to the list to do. There's a technically a fork. But if you want to simulate how something would play out on main net post a certain point or something, I believe there's a feature to do that. Let's see if I can find the docs on that. Or the lack of docs, but somewhere.

33:35 - Tom Haile 
That's like a common EVM development thing is where you just fork a testnet or a mainnet and then dev off of that. It's just kind of a thing. I was just wondering, I know that I've heard people talk about it, but I didn't know how easy it is or how much support that FCL gives for that. And it kind of falls into, the dependency manager as well. So if I don't want to worry about all the dependencies, I'll just fork the chain and then just work off of that, that kind of thing. It's just kind of my thinking.

34:11 - Chase Fleming 
Yeah, this is like, I'd say it's slightly different. I believe you can like, take like a point in time, I think on mainnet or testnet. And this is like off the top of my head. So don't hold me to this description. But and then like in the emulator, I believe. And so it would basically, less about the dependencies, but basically let you simulate the execution of transactions at that point, just to see like what would happen. It was more like for testing.

34:47 - Tom Haile 
Maybe Deniz has a couple of ideas on this.

34:52 - Deniz Mert Edincik 
With emulator, it's possible to work the network. I think it's working on mainnet and testnet. But the thing you said in the, like I am new to this EVM world, but I think the simulating thing on the real network thing, I think it is possible to develop something like this and integrate with FCR. But the main blocker is that we need to convert the transaction into a script and then run this as a script. Um, there are like a couple of things missing on the script environment and like need to be on the cadence and FBM site need to implement this missing things. For example, events are not firing. And, uh, some environment cannot access some kind of Oh, but if we can like before, actually it was possible then. There was some change on FBM. They make some restructure. They break a lot of stuff. But technically, it would be nice to have. Actually, I think someone already did that before on the runner. It was possible. Then I made one version. It was working. Then everything break. But I think it's possible and it would be super useful, actually.

36:25 - Tom Haile 
Oh, nice. Yeah, totally. Totally. This is standard fare on the EDM side. So, okay. Interesting to hear that it used to work and then I guess it broke and then everyone forgot about it. Is that what you would say happened?

36:39 - Deniz Mert Edincik 
Oh yeah, yeah, yeah. It's like it was working. I did something even like step by step going like debugging. But then the environment separated too much. And it kind of stuck like that.

37:05 - Tom Haile 
OK. I'll track that down and see if Pastor Jan has any ideas on that.

37:11 - Chase Fleming 
And then we'll- I just posted in the chat the simulator short description that's on there, just if that's relevant at all.

37:22 - Tom Haile 
Yeah, yeah, yeah. I think, I think we'll need to, need to be, need to be ready. So in testing that Pork and EVM works fine, you know, as expected with the current EVM tools. And then of course we need parity on the, on the cadence side. I mean, cause that's the way DABs work, you know, just pork the chain and start, start going. Okay, okay, cool. Cool. Cool. That's that's helpful. That's helpful. Yeah, we need to get those tools situated so I'll get a I'll get a status of that and then we can we can figure out where to go from there So yeah, thanks. Thanks to this and chase So hey, jordan's back. Hey jordan made it Jordan, you want to give a just a quick status on? All the prs that you had pending for Lintern integration, some VS code stuff you've been working on and that kind of thing. Just a quick status.

38:25 - Jordan Ribbink 
Yeah, good morning everybody.

38:28 - Tom Haile 
Good morning.

38:30 - Jordan Ribbink 
I yeah, so I this last couple of weeks I made some changes to VS code for starters just so that you can switch to the cadence. One might do a CLI a little easier. That way it gets you more integrated with the new linter and the new language server. I'm sure people were already using that, but it just makes the process a little bit smoother. We know about the linter already, but I think I don't know if I mentioned it's in the CLI now as well. You can learn it directly from the CLI. I'm also working at putting some, I guess, guardrails into the staging functionality in our CLI. I've got a PR for that that's just going to need to get reviewed now and it checks using the Cadence Update Checker when you stage your contract. If it's a valid update, it'll tell you if you're not allowed to add a new field or whatever. Yeah, you can disable it because there are situations when you might want to stage a contract that fails some checks, but it's nice to have because, yeah, this way you don't need to wait for the off-chain validation and it just stops people from making mistakes and not realizing it.

39:50 - Tom Haile 
Yeah, and just a note on that the protocol team will migrate all state. And so there's, there's limitations of what can be changed in the contract. I think that should be in Bastion's post, is that correct? Who has that top of head? Yeah, yeah, yeah.

40:09 - Jordan Ribbink 
So it checks against all the rules that they have. And yeah, it might not be bulletproof, right? Because there's no state migration here. So if there's some weird bug, and it's just the simple fact of your dependencies can change later, and this could affect your contract. But it's just like a soft check, I guess, just to catch any simple errors.

40:39 - Tom Haile 
Cool. Thanks. Thanks for the update. I guess we had a few people show up after I brought up the question. Any particular community tools people want to give a shout out to or want to highlight? I know Gio mentioned Flowser and potential Flowser Flix integration. Anybody else? Okay, cool. Cool. Cool. Yeah, I think the Ali, how are you feeling?

41:23 - Ali Serag 
Hey guys, I'm feeling a lot better. Sorry. Yeah. Earlier in the morning, I wasn't feeling so well, Tom, but I got a little bit more rest and now I'm feeling much better. I just had a quick question while everyone's here. So what we're doing is an audit of the core developer platforms in the ecosystem and just checking in on what their upgrade to Cadence 1.0 status is, trying to reach out to them if there's any additional personalized support they need, if they need to get on a call, if there's anything confusing about the timeline or tools that are available or resources. Just wanted to do a quick gut check with the people here, especially Deniz, because I think you worked on what F? It's like a flow view source alternative. I wanted to check on that status and just see with you guys if we're missing anything here. So let me share screen.

42:31 - Deniz Mert Edincik 
It's working. Okay.

42:34 - Ali Serag 
What was it called? FDNS? F.DNZ.net. C.dev. C.dev. Okay. Yes, that's the one.

42:40 - Deniz Mert Edincik 
And so that's already upgraded for PreviewNet, right?

42:45 - Ali Serag 
Yeah. Run.DNZ.

42:57 - Deniz Mert Edincik 
There, uh, I will upgrade it when I find some time, but it should be like pretty quick, just adding the code work. And I have new project still working on this. Not the end of that. It's something like it will take some time because it is like, and also I have. Like runners, some new runners I am trying to make with more script gas limit and not limitations of the private number. So I am working.

43:45 - Ali Serag 
It sounds like you're very hard at work. That's awesome. Um, but now I'm just tracking the existing infrastructure that like developers might be used to or or depend on. So it sounds like the other two that you mentioned, like the FlowRunner alternative, and the other one, those are more net new, right? Yeah, yeah, yeah.

44:04 - Deniz Mert Edincik 
They will be new. Perfect. I am, like, waiting for the stable, like, Cadence 1.0 to launch them. So it will not need to just support the old version, because I think, like, not much time left.

44:21 - Ali Serag 
Okay, perfect. Jordan? Yeah, I guess something worth mentioning.

44:26 - Jordan Ribbink 
There was a community PR pretty recently for Flow.js testing, and by extension, FlowKadoot. I don't know if this was mentioned, but I was looking at usage of FlowKadoot as well, and it looked like it was used maybe in FlowRunner or some of the runners that exist out there. So this may unblock those. I'm not totally sure. But yeah, I just need to keep reviewing that and going through that, but hopefully this should cover it.

45:00 - Ali Serag 
No, thank you for sharing. And yeah, the pull request was from this interesting person named NT Test Alert, who in the last week has been really active in trying to open source things that might be useful related to the Cadence 1.0, related to the Crescendo upgrade, and it's really exciting to see community members get together and support each other. The specific tool that he created was, let me try to see if I can pull it up. Yeah, Stable Cadence Migrator. So it's super basic. Wait, how do I go to the MD? Yeah, it's super basic. And what it is, is an AST and like regex that just goes through everything, tries to statically find all lines that based on Bastian's post needs to be updated. It's not, of course, it's not perfect and very transparent about challenges with it. But like, just wanted to say, like, I was super happy seeing this and seeing this kind of action in the community. Yeah, hopefully you'll see a lot more of this kind of stuff. But anything you guys think we're missing other than like flow cadute, run.dnz, f.dnz, flowrunner, flowview, flowview source, contract browser, float, flowdiver, devwallet, flouser, touchstone, toucans, flowport, da, da, da. Ji? Actually, I think these are the same.

46:26 - Greg Santos 
Yeah, just wondering if, can you hear me?

46:29 - Ali Serag 
Yes, yes.

46:29 - Greg Santos 
I was just wondering if you got any word on FlowRunner or perhaps Denny's getting support for PreviewNet, we can run transactions against?

46:44 - Deniz Mert Edincik 
Sure, I can make it up and running today. It's like, just I need to add one line. That would be awesome.

46:54 - Greg Santos 
I think it's super handy for folks who are testing things out. You can just shoot them at Preview.

47:02 - Ali Serag 
Awesome. Well, if there's nothing that people think are missing here, awesome. If anything comes to mind, don't hesitate to DM me because I want to really make sure that we're tracking the status of everything that developers are used to. Thank you, guys.

47:19 - Tom Haile 
Yeah, thanks, Ellie. The last thing I have on the agenda is any tool improvement suggestions. So any suggestions that would benefit their existing tool base are missing features or anything of that nature. If anybody has anything, just speak up. If not, that's all I got for this meeting. Anything else, any questions come to mind over the course of this discussion? Cool, cool, cool. We can be left with our thoughts. All right, so we'll probably, we'll have another meeting in two weeks. We'll keep this cadence, and we should be able to make more and more progress as the underlining technology gets more firm, you know, as we start doing the migration and testing migration. And, gee, am I correct in protocol is gonna, try to do a migration, I think it's like April 4th or 5th or something like that?

48:44 - Greg Santos 
Yeah, it's still tentatively scheduled for April 3rd, actually, which I believe is next Wednesday. So that would be like the initial state migration. One thing, I mean, I was going to call it out later, but I might as well mention it here just to Ali, like, I don't think we've made any mention of that. So essentially, like looking at stage contracts, it's it's pretty low percentage wise right now. And maybe it makes sense to give another blast if that's not in the pipeline, or just something to say, like, essentially, the initial migration will happen Tuesday. Obviously, it's not the last one, but it might be nice to get some immediate feedback by having some contract stages.

49:29 - Tom Haile 
Okay, good. I'll put that tentative migration test April 3rd. Okay. Excellent. You And I mentioned before, but I'll re-mention again. I consider any kind of smart contracts or stuff like that to be tools, tools for development and all that stuff. So I know Geo's kind of been chatting about some helper contracts in terms of kind of auctions and all that kind of stuff. And we've talked a little bit internal about that. There's a lot of different, Options that can take place. So I would say any suggestions for smart contracts that would facilitate development, then just kind of, you know, bring it up, chat it in, throw it in the 4D, the Discord, then we can talk about it internally and throw some to-dos on various repos or whatever. And Greg can schedule it out if it's in our roadmap.

50:43 - Akos Erdos 
You were showing this project which is helping in migrating in and smart contracts. I was just curious about it. A couple of months ago, I created an AST walker in TypeScript. It's an AST walker, but still with an old version of the KNS. I was wondering, maybe this project could use that AST walker if they don't use any. I believe it was JavaScript as well, based on what I saw when you shared the screen.

51:18 - Ali Serag 
Wait, let me double check what it was written in. OK. Thanks for the link.

51:24 - Unidentified Speaker 
No, no, happily.

51:25 - Ali Serag 
I think that's such a cool idea. Probably what's going to be useful, oh, wait, did I share the right link there? Oh, no, that's Chase's link, yeah. I think it'd probably be more, oh, I think Jordan was just going to say what I was going to say. Jordan?

51:41 - Jordan Ribbink 
Sorry, I don't know if I totally heard the question correctly. Was that about how you can walk the AST in JavaScript, or was it how to use this tool?

51:52 - Akos Erdos 
No, actually, it was, I was just curious about this tool, because a couple of months ago, I brought an AST walker in TypeScript for cadence. It was based on the Go implementation, actually, but my use case required it to have it in JavaScript. And I was just curious because when I was writing it, I was thinking about the same, oh, this could be a great help to anyone who wanted to build any kind of migration tooling in the future. So that was the reason I was asking.

52:35 - Jordan Ribbink 
Yeah, so you can also use the Cadence parser. We have a WASM build. I don't know if you were aware of that. Yes, yes, yes.

52:45 - Akos Erdos 
So with the parser, we get the abstract syntax tree. And then the walker, we can use to walk the trees. And then we can, what I didn't do, any kind of generator. So that would need to be here to be able to. Translate it to a new version or something like that. So that would give you the full chain of tooling at the end. But yeah, I'm aware of the wasn't part of it. It's cool. Yeah, and I just created some lightweight walker, which is just like one piece in the machinery when you wanted to deal with language related stuff. That's it.

53:31 - Deniz Mert Edincik 
I can give some background on this issue actually. Like I tried to write a converter for stable cadence for 1.0 also. Like whoever wants to get into this, it is like a bit fool's errand, I can warn. Because the parser part is pretty easy because parser is almost fixing itself, giving suggestions and like letting you fix everything. It's like takes like one days of work, it works. But the next step, the checker is pretty bad at suggesting stuff. And, uh, pretty bad at like showing the errors. And we have a lot of changes in the NFT, NFT interfaces. So it's like, you need to add like methods, some methods are like changed. And like, it's once you get into this, it's impossible to get it out. You know, it's like, uh, maybe it can fix this pubs, all the accounts and stuff part, but everyone to like leave it there and let people fix it because it's like super complicated.

54:48 - Tom Haile 
Well doesn't the linter give suggestions and stuff like that? I know Jordan had just kind of gone through and kind of helped tease out better error messages.

55:00 - Deniz Mert Edincik 
Oh, yeah, it's like, it is pretty good messages. But for example, like some functions before had like five parameters, now they had like four. And then like, it is suggesting you to change the labels in the parameters to something wrong. It's like, it's really crazy stuff with the interface changes. Like it's, if somebody gets into this, it should be All like all generic core interfaces has to be kept in mind and change them first, then fix them. So like automated is like much harder than like telling user, Oh, this is Emerald fix this. I see what you're saying.

55:44 - Tom Haile 
So there needs to be an order of operations in order to, for the user to get where they want to be. You can't just shotgun it. Okay. I got you. Yeah.

55:56 - Unidentified Speaker 
Yeah, it's a difficult problem.

55:57 - Ali Serag 
I was just going to say, Deniz and Akos, if you guys have repos, whether it's the AST you've been working on, Akos, Or we were just talking about Deniz, and you don't have the capacity, but you have ideas of how people in the community might be able to contribute to them towards helping with the migration. I strongly encourage you guys to just make a tweet about it, open source it, and share it, because you never know if someone's just going to jump in and build on top of it.

56:34 - Unidentified Speaker 
Yeah, definitely.

56:35 - Tom Haile 
And yes, my one is open source.

56:37 - Akos Erdos 
Actually, I can put in the link if I can find it. Give me a second.

56:44 - Unidentified Speaker 
Yeah.

56:44 - Tom Haile 
And, uh, create issues that identify gaps or any particular, you know, hangups and stuff that might, might occur in your repo. And then we can have discussion and stuff and discord and all that. And there, you know, if there's an alignment with the team, you know, the D4 teams, and maybe we can contribute, you know, it's all, all based on what, uh, G has in mind for the roadmap and the direction of the team, G and Ali.

57:16 - Unidentified Speaker 
Yeah, good stuff.

57:25 - Tom Haile 
And I'll put that in as a shout out. Deniz, do I have a link to your repo where you started the migration? Or is that private?

57:42 - Deniz Mert Edincik 
It is currently just main.globe. But yeah, I think that'll be helpful.

57:55 - Tom Haile 
Yeah, thanks. Actually, we got two minutes left. Anybody have anything else, any questions or anything? Thank you. Thank you all for showing up. It was a great discussion. Yeah, very much. Thank you, Akos and Deniz. Yeah, thanks, Tom. Thanks, all.

58:24 - Giovanni Sanchez 
Thank you. Thanks, guys.

58:26 - Unidentified Speaker 
All right. Thanks. Bye-bye.

58:33 - Tom Haile 
Great job, Tom. Thanks. You want to stop the recording right quick?

58:36 - Unidentified Speaker 
Yes.

58:38 - Ali Serag 
Yes, we can. I don't know how to. Do we pick out the AI? Will it record it if we kick out? I mean, I'm going to remove from call and see if it keeps.

58:52 - Tom Haile 
We can just turn off the call. I do have something to show you.

59:00 - Ali Serag 
OK, let's turn it off and just send me a new link.

59:03 - Tom Haile 
OK, all right, I'll send you a link.
