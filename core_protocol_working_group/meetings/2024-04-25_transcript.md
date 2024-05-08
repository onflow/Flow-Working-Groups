# Core Protocol Working Group, April 25, 2024 - Transcript

**Attendees**

Alex Hentschel,
Gregor Gololicic,
Janez Podhostnik,
Jerome Pimmel,
Jordan Schalm,
Joshua Ayo,
Kan Zhang,
Khalil Claybon,
Kshitij Chaudhary,
Navid TehraniFar,
Peter Argue,
Ramtin Seraj,
Vishal Changrani


## Transcript

**Alex Hentschel:**
All Good day everyone Welcome to our second core protocol working group meeting. It's a pleasure to have you all and today. We have a few more I guess mostly reviewing topics on our agenda. So the first thing we're gonna talk about is the upcoming evm gas company. It's a computation limit and the transaction fee updates. citizen Vishal are gonna give us a brief review of what's happening and What you might need to do, if you're developing on the blockchain, the second one is the tuning of the main consensus. So we kind of briefly covered that topic last week the top sub protocol working group met on this topic. Come with various domain experts and key stakeholders, and we want to summarize them.

**Alex Hentschel:**
The details here a little bit. and that's also going to be another 15 to 20 minutes. And then we also have an update on the HD hcu style upgrades for notes software remember? Short reminder hcu is height coordinated upgrade. Those are updates which are upgrades of the notes software or the protocol which don't require the entire network to be down. So that's also topic that leaves us with a little bit of time. We haven't gotten any suggestions for additional topics. But if you have something on your mind you want to discuss, please feel free to drop it in the chat. We can also keep any of the second or third updates a shorter if there's anything important to discuss. So if you want to we can make use of the time and if you don't have anything else work closely,

**Alex Hentschel:**
okay, I think that's it as for the sort of overview and with that I'll hand it over to shetish and Vishal.

**Kshitij Chaudhary:**
Thanks everyone. Alex do you mind if I share my screen I'll just take over from you. Is that okay for a few? awesome

**Alex Hentschel:**
Guys, great. Thank you.

**Kshitij Chaudhary:**
All right, just using some slides that we presented during the governance working group meeting early this month.

**Kshitij Chaudhary:**
So three sort of essential updates three changes, that would be coming to flow with the crescendo launch to start off the first one probably very important for the developer Community is the update on fees. So as you all might know the transaction fee is calculated as a sum of inclusion fee execution fee and then kind of multiplied by the search Factor today the value of the search factor is fixed at one point. but in future the expectation is to make this more kind of based on the demand and supply in cases of network congestion. This might go about one and vice versa for decongestion or sort of lack of demand for the network. It might go down. So when we were thinking about how to kind of

**Kshitij Chaudhary:**
Dodge the fees for evm transactions on Flow. The only change that we are proposing to sort of enable. That is the way we calculate execution effort. So today so far on Flow Cadence. This is how the execution effort is calculated. There are different parameters and different coefficients which are kind of multiplied by these values of different variables based on different transactions. These are of course different and we come up with the execution effort required for that transaction, which is then multiplied by the unit cost of execution effort, which is also currently fixed at 10 to the power minus 8, which is kind of extremely low but

**Kshitij Chaudhary:**
how do we kind of include the gas part on the AVM transaction? This is what we added to the equation. So for an evm transaction that requires 65,000 gas on the ATM network. How do we convert that gas to flow computation units so that we can actually compute and for the transaction. So by adding this there are two sort of variables here one is the evm gas usage which like I said in the examp.

**Kshitij Chaudhary:**
It might be 21,065,000 more or less depending on the type of transaction. We needed a factor that converts that gas into a compute units and we sort of decided to propose a conversion of 5,000 to 1 and happy to kind of go into the details as to how we reach that number. By the way, everything is also available on this forum post that I'll just be pasting the link in the chat. but

00:05:00

**Kshitij Chaudhary:**
going forward so this is our first proposal in the Forum post. And this is again, a sort of a flip ideation situation very early stage proposal. They will be a flip process going forward about this. So that is sort of Number one. The second one is we wanted to allow larger evm contracts that utilize a high gas to be deployed on Flow for which the computation limit of flow was sort of a bottleneck currently. It's a fixed at 999 today. We want to increase it to allow larger evm contracts. So the proposal is to increase this by 5x for now. So there were two there was of course at very direct way of increasing this limit by simply raising this limit to say 50,000 instead of 10,000.

**Kshitij Chaudhary:**
But that would have required a lot of code changes coordination with ecosystem players Etc. So another way to achieve this is indirectly by reducing the execution effort coefficients by a factor of five which effectively kind of increase the computational limit because more operations will now be able to fit in the transaction before the max limit is it and to explain this I'm just like projecting this slide again. So imagine if this was way smaller there would be more functional Loop calls that can fit into the overall execution effort before we hit the limit so similarly for all these coefficients. If you divide these coefficients by five effectively, we are increasing the execution effort limit. But by the way, when we do that, of course that would reduce the fees charged by a factor of 5x as well. So just

**Kshitij Chaudhary:**
Lot of offset this reduction. We would also have to increase the cost of execution unit on flow in by the same factor of 5x. So just projecting this again. So in this equation, let's say this kind of goes down by five since the coefficients have reduced by five. We are simply increasing this by five such that the overall impact on the transaction fee Remains the Same. So that is the second proposal increasing the computation limit by a factor of 5x.

**Kshitij Chaudhary:**
And then finally is the overall transaction fee itself. This does not necessarily have a lot to do with the evm or Crescendo launch. However, there was a flip that was brought out last year which talked about increasing the transaction fee by a factor of hundred based on in improving the sort of the resilience against attacks making sure that in future we have a way forward to reducing inflation by collecting more transaction fees and using those for rewards and finally making sure that flow token utility is competitive against other networks and the ecosystem which by the way we have hundreds to thousands of times transaction fees as compared to what flow has. So again bringing that proposal back to reality or kind of proposing that again along with the other two changes is what we are doing and all these three changes.

**Kshitij Chaudhary:**
Are in post the link. I just shared in the chat. Please feel free to go through this. please feel free to evaluate the impact on you your work your community and feel free to share any questions or even comment on Forum post And vishalif. I may have left out something. Please please add.

**Vishal Changrani:**
No, that's good Thanks for doing this. So yeah, right now it's at the Forum post level where we are inviting people to comment and then eventually there will be a flip out based on this forum And then eventually the flip will be implemented. So that's kind of the process of this whole thing.

**Vishal Changrani:**
That's it.

**Kshitij Chaudhary:**
Yeah, sorry just this one more update. So we're also planning to test some of these changes on preview net before we sort of bring out a more formal flip. That'll just give us kind of more confidence about the implementation of these before we make that formal proposal to the community. We will be posting communication around this and then before we sort of take this life on preview night.

00:10:00

**Alex Hentschel:**
All right.

**Vishal Changrani:**
any questions?

**Alex Hentschel:**
Okay, that is good. Should I move on to the next topic? All right.

**Alex Hentschel:**
Thank you. Beautician Vishal for this for the short sort of summary. I think it's very important that this broadly communicated. So that's the reason why we also wanted to bring that up here. Yeah, I guess such a change is better over communicated and under So moving on to the next topic the tuning the flows main consensus.

**Alex Hentschel:**
So We have a brief summary here of the core protocol stopped working group meeting if you want to watch the full meeting there to recording here but a warning it's I think slightly over an hour long. yeah, but I think the changes can be summarized relatively concisely. I wish you wanted to do here just to also spread the word. So we've discussed various parameters headings into trade-offs between sort of how often we have to do changes under which conditions we have to do changes and sort of speeding up the network as much as possible and

**Alex Hentschel:**
Out as the following. So we're essentially setting the default view time or consensus route time to 800 milliseconds. So at the moment we have 1.25 seconds, so that's a reduction of about 36% So you might remember that. We have one week long epochs every Tuesday. Wednesday, I think at seven PM UTC time we switch epochs and we have a controller which is trying to maintain this default view rate to such that at the end of the week It's been specific number of views past and that the epox which over can happen in time. And with this parameterization of 800 Billy seconds per consensus view we would have about

**Alex Hentschel:**
756,000 views and an Epoch which that's the numbers a system cares about. That's what we have to configure. We have to say so many views and when they are over the new epox starts and of course, with us wanting the epoch switch over to be at a reliable point in time, then that is highly correlated to our individual view or our Target view time.

**Alex Hentschel:**
Yeah until the cruise control sub system as I mentioned already May tries to maintain this 800 milliseconds on the happy pass on average and if some views take a little bit longer subsequent views will be made shorter by the cruise control system and the other way around too. And so the other parameter we need to tune is the corresponding parameter of how long we're maximally willing to wait. So this is sort of on the happy pass we would be about waiting 800 milliseconds, So note enters a new view and then it's like I'm waiting 800 really seconds to hear proposal. And if I don't get any proposal, I'll start to initiate the time out protocol. So I'll for myself will communicate that I have time to all the other notes and propose that we abandoned The View and no longer wait, right? so that this is sort of the

**Alex Hentschel:**
No, how zero is a time where we're waiting or we want to have a proposal by this is a Time 990 milliseconds. That's the longest time that notes will wait on the happy path. If you have successful failures that time will go up out on the happy pass. We usually only have one failure or so because the notes down and we don't want to wait very long, when this town to realize. it's not gonna Respond, no longer no matter how long we wait. And so this parameter is relatively important that in the normal case. a few notes are down the protocol can 6 or proceed very fastly and so we're setting this to 99 milliseconds. There's a mathematical formula which depends which

00:15:00

**Alex Hentschel:**
Which determines the wait time based on the target view time? That's all in the notion dark. If you want to read up on it, please go ahead but yeah, I'm just trying to say that we can't independently choose that the main thing we choose is this value here of the target for your time. So this is how hopefully consensus will behave after the crescendo launch when we'll ship this so for all of you, who are

**Alex Hentschel:**
Participating in the sparking process. I would like to draw attention that there are multiple parameters here. I mean you've already seen two There are a couple more subtle parameters, which I've kind of skipped over here that there are multiple parameters that need to be configured correctly when bootstrapping the mainnet as a crescendo upgrade, I think that is une the mid of June. Yeah, and so we're going to do a practice deployment on testnet, so we're aiming to spark testnet on May. 90 second and there will already practice this switch over of changing the parameter values so that hopefully for mainnet we have a little bit more experience, but if you screw this up, there could be

**Alex Hentschel:**
A yeah consensus could be impacted. So yeah, just trying to draw attention to meeting a clear mind, okay?

**Alex Hentschel:**
I've already briefly touched on the speed ups that were expecting. So in this context, I would like to reiterate the differences of time to finality time to execution and most importantly also point out that there are two different Notions of time to finality. Right so flow is a pipeline architecture here. So it's a excess node collector notes consensus notes and then roughly execution verification sealing and we're tuning is that search that PM the pipeline the consensus step only right? And so you can only look at the consensus and you can define a time to finality. So that is specifically the duration from a block being produced or broadcast to block being finalized. yeah, so we in any time it takes for the block to be constructed or

**Alex Hentschel:**
Transactions to even reach the consensus notes. I'm to be included in a blog and so the consensus time to finality is quite short or reasonably short for most modern consensus algorithm to the best of my awareness. The fastest consensus algorithm is Aptos. They're having a time to finality of around one second and we're roughly a factor of two away from that but including the Slowdown of our cruise control system, if you just let the consensus run as fast as ones. I think we would reach a final of consensus finality times the same as Aptos. So yeah, and with this current update our content or hot stuff time to finality will improve by 36% let's talk about the transactions time to finality which also is called time to finality, but it's suddenly different. So this is measured from the very beginning of the pipeline.

**Alex Hentschel:**
So when the access node first gets a transaction, which is reasonably close to the client sending the the transaction ending up in a finalized block. So at the moment that's about six seconds that will go down to roughly five seconds. And you see already that that is significantly bigger than just looking at the consensus time of finality because we have the access notes and also the collector collectors in between which batch all the transactions into what we call collections.

**Alex Hentschel:**
So I want to point out here in this kind of setting of technically versed people that most blockchains. They advertise their consensus times of finality. So Lana Aptos, they for instance out to say so we have a time to finality of less than one second, but they don't say that's only their consensus time of finality when you look into their system a little bit more closely you find that they also bad transactions and they've left out that batching entirely from their marketing. It's not mentioned and they're actual transactions time to find out as he is reasonably bigger. It's easily two seconds. And so yeah when you hear claims of time to finality below one second be careful, There's usually catch there for flow. We want to go with a scientific the solid definition, which is not on purpose misleading any person who

00:20:00

**Alex Hentschel:**
Is it and when we talk about time of time to finality, we'll talk about that or we mean the transaction time to finality that is relevant quantity for people using the network. Right? I mean, this is an interesting metric about one sub part of the system, but it's much less relevant for user than this year. I mean for us it's helpful because we can specifically say in this setting where we are talking to experts this is specifically say, this part of the system is getting faster and by that much like the consensus part, right, but what really matters for clients of the system it's a transaction time to finality which increases by about or this hopefully will be increasing by 15 to 18 percent. That's our projection at the time. Okay.

**Alex Hentschel:**
last thing I want to go over is the Byzantine fault tolerance and the consensus committees, either that we can support with this parameter setting so we'll change the system to run a little bit faster. That means our margins, if sort of something is delayed or goes wrong are getting smaller. And so when the consensus committee sizes as high is changes drastically

**Alex Hentschel:**
more notes always mean more votes to be checked more votes to be aggregated. So more consensus notes mean the system will generally be slower. The current parameters heading is tuned for contentious committee sizes of something like 88 to 100 notes. We probably can go to smaller consensus and sizes with our problem, but probably shouldn't go to contentious committees this much more than a hundred notes. otherwise we need to adjust the parameters and with this size of committee. our timing will be resilient to about 15% of consensus notes being Offline in our current case or as that sort of them.

**Alex Hentschel:**
A realistic in estimate with some uncertainty or if we wanted to have a more conservative estimate. I would think that at least we can tolerate 10% of offline notes which is quite good, and after that consensus will still continue just that our Epoch deadline will sort of start to drift right because we can't get through the 756,000 views in one week if you have more than 10% of notes of line, so it doesn't break the system per se just sort of breaks the timing convenience of flow if you have more than 10% down and I want to also mention that when I talk about consensus notes being down. that also would include by the time consensus notes so that computation is

**Alex Hentschel:**
Made for actively malicious notes who are on purpose trying to mess with the timing of flow, but since we don't have permission is consensus notes yet. Then the relevant case for us the notes being offline, but we're working on permissionless consensus notes. So once we have a few then it will be nice to know that the system can also handle those notes to be actively malicious. I'll skip over the last thing here time to execution to time to finality. I think I've covered that in a couple of cases already. But if you're interested, I'm happy to go over it again. All right, so that was my topic here on the consensus. Speed up. Are there any questions?

**Alex Hentschel:**
Okay, no questions, then we'll get to the last topic which is also a summary about A zero or no downtime software and protocol upgrades. So here again. We met with a smaller group of experts links to The Forum posts with Jordan wrote a while back to kind of Provide some background and some more specific suggestions on how upgrades could look like meeting notes video from the stop working group a transcript. It's all linked here. If you want to go into details and again here. I'll just quickly go over the key results.

**Alex Hentschel:**
So a few things that we thought is worthwhile highlighting is that the dynamic protocol stage which is more or less the framework mediating those updates that provides us with Primitives for informing all notes. When a new protocol version takes effect and triggering restarts if required you can add custom logic to run upgrade specific Logic for instance if you need to migrate some state or so and the migration is fast, then you can do it just during a restart. With the dynamic protocol State also provides us with Primitives for enforcing consistency across notes so notes that don't run a compatible software version will automatically notices and shut down.

00:25:00

**Alex Hentschel:**
Yeah, so this is also the Primitive Dynamic protocol state provides us for doing node upgrade or software upgrades.

**Alex Hentschel:**
But we want to point out that it's still exploratory. So the dynamic protocol state will reach mainnet with a crescendo update in June and then we have we have a mature proof of concept implementation, but we don't quite know sort of what detailed tooling and convenience logic is useful. So we didn't want to over Engineers this entire thing and focus on certain use cases not knowing whether those use cases are actually really used in practice or not. So this is literal summary from the top working group, which I'll just read out here and so the mechanism under construction meaning the update framework in the dynamic protocol state. So the mechanism under construction is limited to coordinating when the upgrade will

**Alex Hentschel:**
And not the nature of that upgrade. For example, the new software release could understand two protocol versions and be able to switch between them on the fly or the new version could require that the old software shut down triggers the data upgrade process and then a new software releases launched on the new data, but in either case the mechanism will ensure that there is an unambiguous time specifically a view then the new protocol versions activated into all protocol versions obsolete. So this is kind of a summary of what the dynamic protocol state does for you. not you do your upgrade it helps you to deploy your upgrade.

**Alex Hentschel:**
If you want to do a software upgrade protocol upgrade, please come talk to us in this specific case. That is Yuri, Jordan and myself and Khalil will help you to work with the dynamic protocol state, but we won't up implement the specific upgrade Logic for you because that's kind of the very domain specific thing. Right? We see that in the execution notes. It's kind of the minor saying right where the most of the work goes in is. how do I do the excitement creation? How do I do it fast? And that's all stuff where the dynamic protocol State won't help us, okay.

**Alex Hentschel:**
And let me Yeah, and so I wanted to also kind of mention this product angle here. We also briefly discussed that in the prol stop working group. And so we think that The Primitives provided are broadly useful but they're precise impact it's hard to quantify at this point because it depends on the precise nature of the upgrade that we want to deploy using those Primitives and we don't quite know what upgrades we want to ship within the next 12 months and how urgents they are. Right? And so this is a quote here from deed and he says, I don't know but it's inconceivable to me that this is not useful and valuable in the next 12 months to release software that at least we care about releasing and more easily release that software. so I hope this kind of provides a brief summary here.

**Alex Hentschel:**
Last point I included to make to say that it's not quite easy for us to say. it will for sure save us a spark or maybe not but we generally think it's useful and it's a very good work to have done and having those Primitives available. Even though we can't quite precily say we'll use it for upgrade XY and that was the part I had on this topic. Are there any questions?

**Alex Hentschel:**
Also know that's great any other topics you want to discuss? You can drop them in the chat or just speak up. Jordan go ahead, please.

00:30:00

**Jordan Schalm:**
Yeah, just briefly. I wanted to call out. Maybe I will drop a quick link here. And I can put this in the meeting notes, too.

**Jordan Schalm:**
I'm kind of on a similar vein to what you're talking about with a dynamic protocol state. This is thanks this is a proposal for slightly revived revising Service events. In particular I'll give a brief background about what this audience with the dynamic protocol state. It makes it easier to change fields in the protocol State like protocol parameters things like that. Often by a kind of ultimately resulting from a governance transaction so we kind of envisage this pattern going forward where we want to change protocol parameter.

**Jordan Schalm:**
Without needing a pork or ideally without needing a software upgrade and we get the governance Community together. They can sign a multi-sig transaction to change the protocol parameter or whatever. We want it that can trigger this thing called a service event in Cadence, which if you don't know is a special event that kind of gets hoisted out of the execution environment by the execution nodes and gets transmitted. Through the protocol layer to the consensus committee, which processes it when deciding how to mutate the protocol state. when it's processing a block so Service events are kind of the way that smart contracts and Cadence in particular systems. Smart contracts can talk to the protocol State and the consensus committee.

**Jordan Schalm:**
So we envisage this pattern where governance transaction figures a service event, which triggers a protocol parameter change or something similar in the protocol state. And we notice that There's a constraint existing with Service events as they exist now, which makes that not impossible, but just quite onerous to do. rather than just having the transaction itself be able to emit these events. You need to have that transaction. Store some data to the contract storage and then you need to have what we call system chunk which is a thing that automatically runs.

**Jordan Schalm:**
Runs every block pull that thing out of storage check and see if anything's changed and if so, we met a service event. So it just kind of requires adding a lot more code and flex D every time we want to do this pattern which we kind of imagine that we'll do more frequently. The reason we had this constraint to begin with is just to kind of tighten down as much as possible when and who can emit Service events because they're highly security sensitive. But overall we think that it's not worth keeping this. So This document here goes over the reasoning a few people of China and in comments most people it seems like have agreed on the suggestion, which is removing that third constraint for what qualifies as a service event.

**Jordan Schalm:**
But yeah, so just calling it out here in case anyone would like to participate in this decision. At the moment we kind of have agreement on going forward. So if there's no other concerns from anyone about making this change. We will most likely incorporate this into the EFM recovery work stream.

**Alex Hentschel:**
Thank you Jordan. you bring a topic. Very nice. And I also wanted to encourage everyone else to bring topics. If they have some either in this form, just show up with your topic. I'll start doing a short at the beginning of the meeting. just collect topic that you maybe want to discuss so that I'm not biasing the discussion was now on topics that I bring so I'll do that. Of course, you can also always open NPR on those stocks here. it's just in GitHub on those agenda usually exist a few weeks ago and just open NPR to add an item if you want to or bring it today, that's great.

00:35:00

**Alex Hentschel:**
Yeah Vishal correctly.

**Vishal Changrani:**
All one quick question for Jordan. So this change is an extension to the EFM design, right? We just kind of like This is a part of the whole EFM recovery design, correct?

**Jordan Schalm:**
It's not really. A part of the EFM recovery design specifically. It's just that one of the features of EFM recovery is adding exactly this kind of governance transaction. So we were going through the process of implementing that and we were kind of noticing. we need to do all this extra work. We actually did it twice for this and then also for the protocol version upgrade that Alex talked about the third item So it's not really. Super related TFM recovery It just fits nicely and with that work because it lets us simplify a part of the implementation of it.

**Vishal Changrani:**
What? But thanks.

**Alex Hentschel:**
Yeah, thanks That was very good question. it's more like a thing. We keep pumping into and one rank if you should change it and I think now it's probably a good time to change it because we're gonna have a lot of those bumps otherwise Great any more topics things you want to discuss?

**Alex Hentschel:**
Otherwise, I think we all get 20 minutes back. Thank you. Have a great day and hopefully talk to you in a month.
