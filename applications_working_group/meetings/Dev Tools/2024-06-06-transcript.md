Dev Tools Working Group (2024-06-06 10:08 GMT-5) - Transcript
Attendees
Akos Erdos, Alexandr Ni, Ali Serag, Ali Serag's Presentation, BoHao Tang, Chase Fleming, Deniz Mert Edincik, Jack Forgash, Jack Forgash's Presentation, Jordan Ribbink, read.ai meeting notes, Tom Haile
Transcript
This editable transcript was computer generated and might contain errors. People can also change the text after it was created.
Ali Serag: amazing
Tom Haile: nice
Ali Serag: All So first session just recap we discussed how third parties such as Flipside and make sense to access different types of data and for different use cases and create these different apis. We kind of started to explore. what was available on the flip side. there is an awesome data Studio that Jack shared with us. It's pretty easy to write various types of queries and you're also able to generate an API endpoint that people could include in their app and start building out interesting dashboards or use cases and it's based on this API structure where you pay for usage when it comes to
Ali Serag: What's available from? find
Ali Serag: where we're at is just I kind of went through each of them individual with biarte and Where we are with getting token prices is it's not ready, but they're able to make it.
Ali Serag: Getting historical token prices or balances for an address. It'll be possible after Cadence 1.0 same thing for getting lunchable token holders at a specific time or block height getting historical prices over time. It's available right now due to deck screener like coming in and requiring an adapter for their API, which
Jack Forgash: For those balances what do you mean when you say to be available postcadians 1.0 is that with new methods that are being deployed on the contract upgrades or? Yes. Yeah, how
Ali Serag: they're building something through a names project that they're working on that will facilitate it then
Deniz Mert Edincik: A little bit I am talking all the time with Piet and…
Jack Forgash: Okay.
Deniz Mert Edincik: they will index the storage. As far as I know but they will start maybe from post. creation only
Ali Serag: Yeah. Yeah, so long story short when it comes to what we're like accessing various forms of this data, a lot of it will be coming through find post Crescendo one exciting thing is the historical prices because that will open up a ton of different applications in What I mean by that is like if you're creating say a crypto Index Fund you would want to be able to aggregate the historical prices of beaver token of Worf coin of frug. And if you want to create an index that has all of those slices and see the past historical performance of that so you buy a token that has
Ali Serag: Underlying assets representing different percentages of that vertical like defiant flow you need to have that historical price information to be able to see how it performed. So being able to take the data directly from increments gonna be an exciting area and I believe through the conversation that things that are essentially the integration that deck screener as has unlocked, collaborating with increment five at the same time to do that as unlocked a lot of new interesting sources of data. Yeah, any questions on this there was also some follow-up I had with side. On some different areas that we want to build out and work on.
Ali Serag: What I'm envisioning right now though is what the end to end path looks like for developers that want to be able to make very simple data queries. if I want to come to flow and I want to make a data snapshot how do I go end to end from landing on flow.com or going to the developer Docs? Does anyone have any ideas in that area?
Ali Serag: On what the flow should look like?
Tom Haile: It's the one more time the flow specifically for what?
Ali Serag: For data access so figuring out if I'm a er I'm doing a hackathon. How do I and I want to do a very simple query I want to get a snapshot of token holders at XD. What does the user Journey look like in your guys opinion end-to-end?
00:05:00
Tom Haile: There are we talking about right now or after Crescenda?
Ali Serag: No, no after Crescendo and the ideal and the ideal world.
Tom Haile: I think there is no solution. And it needs to be built.
Ali Serag: It does need to be built, but I guess. To make it more tangible and we kind of touched upon it just a little bit last time.
Tom Haile: That's a good looking landing page you get there.
Ali Serag: A great developer built it out.
Ali Serag: What I have in mind is either in in the network section of the developer dogs. You're able to see accessing on chain data. And when you click on that you'll be able to essentially.
Ali Serag: Very easily figure out what types of data you'll be able to access and where to go. For example, we would link out to flipside's API and we have a list of the most common type of workflows things that developers want to access and similar thing for flow diver. I'm not entirely sure if there's going to be any differentiation, but I'm imagining that we would just list out all the things that are possible and then the different third-party providers in the ecosystem that they can go to we wouldn't elaborate on the payment schemes that these third party providers offer or how many API calls Etc. We would just be …
Jack Forgash: yeah, I think so for us
Deniz Mert Edincik: I think maybe it's somehow we need to group them in some kind of capabilities…
Ali Serag: flip side offers this sweet of apis and a custom like Studio Builder to query data on chain using SQL and…
Deniz Mert Edincik: what they can do. And say that for example …
Ali Serag: generate API endpoints for you to aggregate data directly inside your app.
Deniz Mert Edincik: if you want historical data.
Deniz Mert Edincik: Go this way…
Ali Serag: How does that sound to you guys?
Deniz Mert Edincik: if you want.
Ali Serag: Does that sound like a good path?
Deniz Mert Edincik: To create something about transaction histories like protocol state. You have this options if you want to do something you have this options…
Ali Serag: Mm-hmm
Deniz Mert Edincik: because there will be a lot of options, but I don't think either flip side or find or somebody else quick notes. They will not support all of them. So it's like we need to have some kind of metrics of stuff like this provider supports these things so if we can give them this Capabilities I am calling but I don't know the word exactly that they can do a features or…
Tom Haile: as feature
Ali Serag: Yeah.
Deniz Mert Edincik: better and in this feature sets we can say that also it will be some kind of motivation for the provided to implement more features. When it was gross metrics like this.
Tom Haile: I have a question. it's Our Canon archive node, make queries per block height going back. However far Or does the data need to be consumed and stored in a certain way to run these snapshot queries that might go back two or three months.
Deniz Mert Edincik: I can answer this access notes are doing what before this archive notes are doing this. They can query from the state I think from beginning of Crescendo to Forever will be But the problem that is this data is And archived not access notes and…
Tom Haile: right
Deniz Mert Edincik: not indexing them. so probably some third parties needed it is not easy to index to it is pretty complicated I made the proof of concept after I talk on last week. it is indexing, but it's taking a lot of time to build that stuff.
00:10:00
Ali Serag: awesome I guess.
Tom Haile: All So archive notes node is not the answer is what you're saying. So you're saying a third party? Needs to build a specific service.
Deniz Mert Edincik: Yeah, yeah. It's archive notes for Not the answer on this.
Tom Haile: Okay. Okay. Thanks. Yeah, that was my curiosity.
Jack Forgash: Yeah, the HTTP API is very useful. But I think that is only for the current spark for anything in a past archive note. I think you'd have to make grpc calls, which then is another level of abstraction away from simplicity. So yeah within a full index data set what we have we hit all of those. I think we're
Jack Forgash: yeah up to the candidate 7 I think was earliest one list there are some of when we set it up candidate 7 was the earliest one listed on the past Forks docked page as these six five and four are also available now, maybe we'll hit those as well. But yeah, we've gone through and made calls to blocks collections transactions and transaction results so that from the entity review we have at least all of that data available in Flipside so that if you wanted to, take a look at activity based data queries. For something, significantly in the past and you can go through that. But if you're trying to make calls like, the account and point or executing script Addison block of time with the HTTP API that's best on that chain head.
Tom Haile: That you got you.
Ali Serag: On a tie it back to the feature sets for developers that are interested in accessing on data.
Tom Haile: Thanks.
Ali Serag: What kind of feature sets do we imagine at? This point might be interesting to them?
Deniz Mert Edincik: I think It's splitting into two a sort of I am little bit like today with the bed internet.
Tom Haile: I think go ahead.
Deniz Mert Edincik: I think that it's splitting into two states in the global blockchain one is larger state. the storage what you are storing the second one is protocol State what Jack mentioned before me this events or transactions or blocks? so I think we can split into two somehow like protocol State and later State and under them. We can feel for example Accessing other stuff all can be done on the flip side. I'm fine. They are almost I think same thing that all but on the other side Ledger side. Currently we don't have I think nobody.
Ali Serag: What would we want in the future Under The Ledger side?
Ali Serag: because
Ali Serag: what's the current way if you wanted to find the owner of a specific resource that you would do.
Ali Serag: Currently there's no way.
Ali Serag: Okay.
Ali Serag: I like this so I like breaking this down into this feature set Matrix and then showing different Partners in the ecosystem and places that you could go to query data and having pros and cons if you want to simple apis to be able to do X Y and Z go here or go there in terms of find. I asked what is currently live today and they have this historical API that I think some of you guys have seen before actually has anyone used this before.
00:15:00
Ali Serag: unhistorically Okay,…
Tom Haile: I have not.
Ali Serag: it's pretty basic you're able to acquire things related to blocks events transactions taking rewards Etc. There's not a lot. I haven't played around with it. But this is what they have right now. And I think that this is something if we wanted to get something up and live before. Crescendo then we could literally just start talking about the data suit Studio on Flipside and then we wouldn't be able to do the full set. I think of workflows that we identified but we could get something up and running right now. that's a basic subset. Along those lines. I'm happy that Jack is here.
Ali Serag: Which of these are we able to do right now with? Flipside Jack in terms of the easiest cases
Jack Forgash: And I was looking through Either this morning admittedly as I was outside. Welcome my dog. Can I share? I just have a note of that.
Ali Serag: Yes. Yes, please.
Jack Forgash: Screen too, I think is right.
Jack Forgash: So just going through. Yeah, kind of catry by category the first one being addresses. So in my research here, you could definitely estimate and address for either the flow balance or fungible token balance from, count Genesis to a point in time by attracting inflows and outflows that gets expensive. We have tried it with blockchains in the past. So we have some partners that are trying to do this right now. it's a good way to estimate but I don't think it's a good way to build something. That is very robust. and then for flow and fungal token, there are two ways we could make calls direct to nodes with the flow balance type of thing. We'll be getting account by address that does include a
Jack Forgash: An account balance with it for flow. However, I found with this one. of course works. Sometimes passing a past block height in right now. We're getting at that block a balance but when I did it earlier, we'll get an internal server error. And if we want to go beyond what is currently, accessible in the access node, there's a cache of to go back to block 75 million still in the current sport. However fail to get it from the execution node because the data is flushed to the access So definitely a limited resource available by using this. so potent for go forward. Yes, we could set something up and kind of query once a day or once an hour for accounts, but getting historical data definitely gets more difficult.
Jack Forgash: Kevin said you could maybe pair a trans inflows and outflows with a go forward of this and try to reconcile okay, we started this pipeline as of today. Maybe we'll figure out how to backfill by working with some of the infrate team in yeah,…
Ali Serag: mmm
Jack Forgash: Seth reconcile the two so that's slow historical token balances. Similarly. You could do that that also gets very expensive especially with fungible tokens. I started playing around with making calls direct to the scripts to get balances. I'm not very good Cadence. I'm pretty new at this. So I think I picked a bad contract with that the USD not that it's bad contract, but when I tried to take this method and apply to other contracts, it was not transferring because I think at the USD is a pretty early deployed vulnerable. So in calling this I could get a balance back and one thing I did not Showcase in that call.
00:20:00
Jack Forgash: The presentation was live query which is post request within SQL obviously SQL is not a scripting language. So it gets a little bit limited but we do have a UDF which sends API requests. So this one to I think it's just the flow script endpoint. You can basically just paste the Cadence that we want to call here into it and then within a SQL query get a response to this balance at this point in time was 0 f USD I said that if you're building a query where you have a handful of balances that could work in SQL out beyond that would need a pipeline set up…
Tom Haile: but Yeah a question.
Jack Forgash: but there are potentially ways to Build pipelines that get balances directly on Jane by calling these States from the Cadence deployed contracts definitely decent lift…
Tom Haile: I assume you'd want to after you do a base of balances, I guess for perfunctory or whatever. Then you could just consume events when funges are transferred and then only update whenever an event comes through.
Jack Forgash: if it can be generalized across modern fungal tokens,…
Tom Haile: so it
Jack Forgash: I should have started with them recently deployed one, then it would make things much easier. I'll continue to take a look at that. It kind of depends on priority.
Jack Forgash: That's balances. It's taking positive for second.
Tom Haile: the snapshot Yeah, it makes sense. and it would be interesting,…
Jack Forgash: Yeah, that's a good point.
Tom Haile: To Ali's question is you want a particular fungi.
Jack Forgash: No, if we have a baseline of okay, this was the balance directly from node each day. We can kind of take a look at this individual tree had this outflow in that 24-hour period reconciled against the next 24 hour call to get that balance.
Tom Haile: Balances across the accounts at a particular block. So then you just go get all the tangible tokens from block whatever back to fill everything up…
Jack Forgash: to kind of you have that.
Tom Haile: because you are only interested…
Jack Forgash: State of true…
Tom Haile: if you only do incremental saves Per account that changes…
Jack Forgash: what I say here? The point of Truth snapshot. Yeah.
Tom Haile: then you consume. probably from The block that the fungi was created so you probably need that up until whatever the block snapshot that the user is interested in and then you could fill that whole state for that particular fungi. the
Tom Haile: it's kind of interesting as So you need to consume a couple of different events. and the access notes are pretty slow. And the API calls get pretty slow. That I have found because I've had to hit the thing. A lot fairly recently. so you want to minimize the vehicles, of course.
Jack Forgash: Yeah.
Jack Forgash: For And it's definitely something we It would be a big Bill but we can definitely dedicate resources to it. We've done this for ethereum. We have token balances and eat balances. So, user address what the token contract is balance at, certain blocks. So it's an area that
Tom Haile: Have a question for you. Do you have a simple for the EDM side?
Jack Forgash: we've done before and I think with ethereum here we did something similar to what I'm talking about…
Tom Haile: It's just an API call to get all the fungi's.
Jack Forgash: where it's okay. Let's, call to get balance from each contract that's deployed that we want to look at.
Tom Haile: Token addresses like hey,…
Jack Forgash: Two years ago we were looking at that,…
Tom Haile: just give me all of them.
Jack Forgash: can we infer based on outflow and long ago decided that is just a bad approach too expensive to brought with theirs too many kind of replays required,…
Tom Haile: yeah, first question is just give me all the contact addresses.
Jack Forgash: but can definitely be done.
Tom Haile: I'll go grab all the metadata…
Jack Forgash: It's a big lift, but we can do it.
Tom Haile: but second question would be hey give me all the metadata as well. That would be great. Just to fill in UI.
Jack Forgash: Yeah.
Tom Haile: So basically I'm putting fungible tokens in flow port or the case side for the EDM side, and I need an indexer. It's got it and so we'll work it. We're kind of researching that.
Jack Forgash: balances or the tokens and metadata and the simple name would I guess what's the question?
00:25:00
Jack Forgash: Gadget
Jack Forgash: From that side of thing like our data science team will go and Pull and labels. So we'll Not the first one you asked about but most of the labels are centralized exchange deposit addresses, but then they're also be a lot of tokens and contracts that are deployed.
Tom Haile: Except it's cool.
Jack Forgash: So low.
Tom Haile: And I assume you'll pick up bridged assets as well.
Jack Forgash: dim contract Yeah,…
Tom Haile: So evm addresses that get bridge to Cadence is not a big deal.
Jack Forgash: so Jim contract labels will be just kind of like pulling from events.
Tom Haile: But Cadence assets that get bridge to DVM side.
Jack Forgash: What contracts are we seeing people actually deployed and…
Tom Haile: They should show up with their own evm address.
Jack Forgash: can we just basically align the account that deployed it with the contract name?
Jack Forgash: And then the labels is our data science team is going in this data sample get back, 10 centralized exchange addresses, but there are also contracts in there whatever metadata we can pull about them.
Tom Haile: I hope Event gets admitted.
Tom Haile: Yeah, So there's an internal Bridge or flow so users will be able to move assets back and forth from the Cadence side to the VM side.
Jack Forgash: For Bridges right now. when you're
Jack Forgash: yeah.
Jack Forgash: Yeah, that was like I think everything is gonna require every work. One thing. I'm turning on testnet this week to take a look in the money VMS up will turn on testnet for that too in just our silver model so I can take a look at how everything's interacting because yeah right now sealer and blocked Bridges, are the standard Bridges to get in and out of flow and we do have that mapped out. I'm just with the events that are admitted to kind of look at outbound tokens. How much where they're going but yeah once evm is live on Flow and there's that intra account for us environment bridging. What it will be mapped in some way. I don't know what it looks like yet.
Jack Forgash: Yeah.
Jack Forgash: Yeah, absolutely. Yeah, so I didn't mean to hijack. so yeah other stuff that's available. The prices we pull from coin gecko. I also have a model up that probably may need a little bit of love and rework that does some price inference based on swaps easiest with stable coins when you're going from you…
Ali Serag: Okay, just elaborate. So you already have it set up to pull in historical price data tokens on coin gecko,…
Jack Forgash: 100 usdc to you…
Ali Serag: but you want to incorporate the tokens on incrementify and…
Jack Forgash: I don't know 105 flow you Converse very easily.
Ali Serag: the prices from those as well or…
Jack Forgash: So I'm very curious to see…
Ali Serag: do you want to use that as a template to do one for increment file?
Jack Forgash: what increment was gonna make available potentially, if that's another source that we can bring in and make the pricing data or…
Ali Serag: Okay.
Jack Forgash: bust that price is pipeline gotta be overhaul about three to four weeks ago. So it's far more robust, and it used to be and we go back basically as far as possible. token holders
Ali Serag: cool
Jack Forgash: 
Jack Forgash: So it pull in increment alongside it depending on what they have available. If that's an API that we can just set up a pipeline to if it's contract calls and setting up is some sort of execute script permit it it should be API.
Ali Serag: Okay, cool.
Jack Forgash: Yeah right now go gives us you have this new asset metadata table for what's the deployed contract address, some metadata for it and the
Ali Serag: Cool
Jack Forgash: And the actual price for it? I have Source in here.
Jack Forgash: And then we kind of flatten all that into just one per hour open high low close.
Ali Serag: No, no. No, this is exactly what I like we need to do we need to map out what's currently available right now. What would be low lifts to add and what we can add in the future because if we're gonna…
Jack Forgash: Yeah corn gecko we decided.
Ali Serag: if we're gonna add a path for developers to the docs right now,…
Jack Forgash: Right now they seem to have the most robust data set available with the most reasonable API.
Ali Serag: we can take an incremental approach and guide people to flip side…
Jack Forgash: So we pulled in everything that we could
Ali Serag: but paint out a longer term picture. So what we're doing now, don't feel your hijacking. It's good to go in depth here.
Jack Forgash: thank you kind of go quickly these because like I said feel bad for hijacking token holders.
00:30:00
Jack Forgash: Okay.
Jack Forgash: Okay, cool. And it helps me kind of prioritize, how to continue data development with flow and making sure that it's up to what the community needs.
Jack Forgash: And it token holders. I think that's similar for balances right now where you can invert from activity inflow outflow. I have not yet looked at contracts to see is there a similar,…
Ali Serag: Okay.
Jack Forgash: get holders basically on some stuff that I've worked with with for example, you can kind of a get accounts and point in many contracts. It'll tell you it'll just return basically a big array of account as the key and balance as the value. That would be my next step is to take a look. Is that something we can call the contracts for and then basically index the result of that?
Jack Forgash: TBD that would be in a similar vein as balances.
Jack Forgash: Some of these definitely get bespoke nft metadata. We kind of Get By Priority really we've had Outreach with the all day and Topshop teams and have access to the graphql endpoints and have pipeline set up for those. they also push data on chain when new moments are created. So that's something like when it actually emits an event. that's in the data set anything can be pulled and curated.
Jack Forgash: There's I think one or two more right now that are doing that in a clean way. they can't remember off the top my I meant to look before this meeting the UFC Strike Team wanted to do a drop with us. So they provided to dump at the metadata and script of what they used to pull it from the nft contract that I could set up with that, execute script it endpoint and start to pull in and automated way when we want to turn that into something that updates itself. Yeah other projects DVD it All the metadata tends to be accessible in a different location and…
Ali Serag: Okay, cool.
Jack Forgash: from a different method. So There's a capacity.
Jack Forgash: It's a capacity issue. Frankly. We have some if we want to like Disney Pinnacle. That's not something we support right now, but we could look is this unchain can we get it from the contract? Is it require an external API? That is still what bespoke process of let's find out where it is. how much lift it would be to incorporate it and Where does it slot in relative to everything else?
Jack Forgash: Energy floor prices and We have a sales table. Very robust flow burst use it in there stats page right now in building that. for a completed sale, I only care about a completed listing but there are plenty of events that are admitted when someone creates a listing when someone closes a listing without a sale wouldn't take much SQL to scan through the events table find those and…
Ali Serag: Okay, awesome. So if I wanted to break down everything here and…
Jack Forgash: then assign, contract price…
Ali Serag: apologies for the redundancy into what's available right now and…
Jack Forgash: if you wanted to determine the floor price of …
Ali Serag: then what would be a low lift?
Jack Forgash: what people are listing it at and then compare it…
Jack Forgash: what people are selling it at sales table and obviously easier…
Ali Serag: To add …
Ali Serag: how would you break that down based on these two?
Jack Forgash: that's pretty curated but the events table those are admitted and very possible to get And then transactions for address transactions and time range. Those are kind of some of the base core entities in the fact transactions and events tables.
Ali Serag: Okay.
Jack Forgash: bottom available now
Jack Forgash: owners available. he could look at mints and sales and kind of infer it from has someone bought it or minted it but not sold it or burned it. definitely computationally maybe a little more expensive than just being able to get holders from the contract but attitude metadata possible for
00:35:00
Jack Forgash: all day Topshop strike anything else that posts their metadata on chain, which two years ago? No one was doing now. We see a lot more projects doing so that's an okolazos. That's what was I could go as us posted on chain as well. Yeah, if they post it on Jane wanna met editions created easy. We pull it out of events and clean it. token holders. can be estimated and inferred computationally expensive, I'd put that in the bucket of balances of It's possible. Do you want to do it? Probably not you're gonna burn through credits. It's gonna take a long time if you're trying to do it for every address across flow since block. 7.6 million, which is the first one main net one. It's gonna take a while.
Ali Serag: You mentioned getting the talking balance. You could get the estimate right now. Would it be more precise after crescendo?
Jack Forgash: We could build out some methods to get flow balance and fungal token balance by address by calling the API or…
Ali Serag: And Why are we able to only get estimates that exact amount…
Jack Forgash: on chain methods. with moderate to high lift,…
Ali Serag: if you don't you might be a dumb question, but once
Jack Forgash: but it's possible.
Jack Forgash: And prices exist we can supplement and add anything increment has an index it alongside. What going gecko has for sure.
Jack Forgash: I don't know.
Jack Forgash: Also it depends on. kind of like
Jack Forgash: the flow so What you can do to estimate is because they okay and certain point in time. I swapped flow for usdc. There's a whole bunch of stuff I could do with it. The token transfers table does its best to estimate all those flows. So we look at every transaction and kind of look at all the tokens withdrawn tokens to positive events and determined that that is a transfer doesn't matter. If it's a swap doesn't matter. I'm sending it doesn't matter if I'm burning it.
Jack Forgash: if it's a swap that'll be in swaps table, but it's a type of transfer in a way. However it's possible that the methods we're doing to determine transfers like that or not. Perfect. So if I do something that is non-standard that doesn't use sit tokens withdrawn with it don't know if it's possible that happens then maybe it's missed and then there's a delta in the balance but then also the eight of us and none of us on the call right now, that's nine accounts across all those blocks. So we have to pour through it gets very competitionally expensive to do that. And then let's say there's
Jack Forgash: Okay, we determined that there was a bug in here. Let's go add it back. Let's replay everything that we've done and rebuild those from scratch to account for this, bespoke type of method that I think slow and this is a credit to flow does do a better job of standardizing methods than many other blockchains…
Ali Serag: No, that sounds good. So I don't want to put you on the spot for…
Jack Forgash: because of I don't know I think maybe contract inheritance.
Ali Serag: how but are there any common workflows?
Jack Forgash: There's a lot of other blockchains we'll just be like,…
Ali Serag: And this is also applicable to and…
Jack Forgash: the si this developer want to call this one token deposit and…
Ali Serag: as well the bohao. I know you've worked on a lot of hackathons with a lot of hackers in the past with flow.
Jack Forgash: the third one and call it deposit token. Whereas it's a little more standard here. there's all sorts of bespoke nature that could come in where something could potentially be missed that. Maybe we have to go back in and add support for that.
00:40:00
Deniz Mert Edincik: Probably the properties if it was fungible token. maybe some balance history in this block height the balance history of this account for this type was this and that. Are the only things needed.
Ali Serag: I think
Deniz Mert Edincik: we have to two directions one is resource or account specific and history by time for example your accounts flow balance. over time another dimension is one resources Journey over time if it was over time to reach users it went
Ali Serag: okay, so the historical ownership and transfers that occurred with that specific Resource as well as the balance I agree. Those are the only things on chain that you could get with it or that makes sense.
Ali Serag: So what I'll try to do then is based on all this information try to make a low Fidelity doc that we could potentially add to the developer docs that include a type of Matrix and then during the next working group, we could review it together also reach out to people individually to get their feedback before then. But the whole idea of this is working together with the working group and the community and the internal team to flesh out these types of paths and build together. So I think this has been really really useful.
Deniz Mert Edincik: I have some ideas…
Ali Serag: Is there any other areas things that popped into anyone's Minds that they think is relevant along this state aquarium and…
Deniz Mert Edincik: but it's like for example something would be nice…
Ali Serag: access path
Deniz Mert Edincik: quick notes takes this and somehow. Little bit implements on the access notes. I'm like advancement and…
Ali Serag: I feel like out of everyone on the call.
Deniz Mert Edincik: for example,…
Ali Serag: Probably Dennis has done the most in this regard of accessing on chain data to build things.
Deniz Mert Edincik: I can create this data with this within the scripts in Decatur would be super nice. And would be super useful probably because Cadence devs. using something on the scripting side and using this API is directly inside from the scripts would be super useful.
Tom Haile: I think It's interesting…
Ali Serag: Yeah.
Tom Haile: because I would say That the Cadence resources are fairly Limited in the ecosystem.
Ali Serag: mmm
Tom Haile: So having apis arrest service and all that kind of stuff. I think would be more broadly available to the existing developer base. But I can see your point.
Ali Serag: interesting
Tom Haile: but in case just on chain data and you're saying you want to broaden the scope of cadence and Scripts.
Deniz Mert Edincik: Yeah, it's a lot of times when I am writing scripts or something in the Cadence. it would be useful to access this data. somehow from inside the Cadence for the Cadence developer, of course, but somehow calling this API if access notes not provide those providing this API or somehow they can somehow integrate this into their products.
Deniz Mert Edincik: Would be nice.
Tom Haile: Yeah, I see. That would be really nice. It's interesting. I'm not sure the scope of quick note. I assume they just run notes. I'm not sure they have any development resources. So
Deniz Mert Edincik: Yeah, they're little. I don't give too much time for that. to serve
Tom Haile: Yeah, yeah true true.
Tom Haile: Yeah. is there I'm wondering from the axis node API. So they're going to be able to run scripts on the access notes itself. I'm not sure when that's gonna be pushed out, but there's also taught.
Deniz Mert Edincik: I guess. Yeah, it's always out…
Tom Haile: Okay, then there's all.
Deniz Mert Edincik: but not activated or there's some kind of like a fallback mode if some error happens.
Tom Haile: 
Deniz Mert Edincik: It's still going to the execution not. But it's already a long time.
00:45:00
Tom Haile: Okay.
Tom Haile: Okay, that's good to know and also they're gonna reduce the compute per script.
Deniz Mert Edincik: Yeah, this is challenging leader. But this is also good opportunity for the providers to step up and…
Tom Haile: Yeah, exactly.
Deniz Mert Edincik: allow high and limits for some. compensation
Tom Haile: Yeah. Yeah, that makes it that would be funny if running scripts cost flow.
Deniz Mert Edincik: yeah, it's totally possible
Tom Haile: Would be less likely to run a lot of scripts. I guess you'd say so that would be one.
Deniz Mert Edincik: in currently it is unsustainable it's construction create compute unchain
Tom Haile: Yeah. That's true.
Deniz Mert Edincik: not easy.
Tom Haile: Yeah, so, hence, we're talking about data availability.
Ali Serag: either
Tom Haile: So data's not free. and…
Deniz Mert Edincik: Yeah.
Tom Haile: in the web and the web 2 world, it seems free. even though everyone's just paying AWS, but Trying to create that same environment on the web 3 is challenging.
Deniz Mert Edincik: but follow is very capable on this You can do almost anything with cadence and…
Ali Serag: 100%
Deniz Mert Edincik: current model. I even like sometime ago streaming videos and stuff. So
Tom Haile: Yeah, what's the dentist? Maybe what's the current state of the light node?
Deniz Mert Edincik: light notes I Observer not …
Tom Haile: Yeah, it was called the Observer node.
Deniz Mert Edincik: yeah. it is not so good. But I have this tiny and If you are interested, it is almost excess notes.
Tom Haile: I'm just
Deniz Mert Edincik: but it is very tiny
Tom Haile: It would be interesting to have a memory model like an access node in memory.
Deniz Mert Edincik: in memory in what sense?
Tom Haile: Yeah, I'm just thinking, way back in the day. We created a memory database for web apps that would do the sinking with the blockchain, on a worker thread and so the UI would just talk to its local database that's in the web browser. And so the embedded Sinker essentially was an access note to some degree, but it would do all the sinking and it would handle snapshots and it would make the data available for the user in their browser instance. And I don't know I was gigs it could be fairly large.
Tom Haile: From that respect the day the user's only really interested in their own data.
Deniz Mert Edincik: Yeah.
Tom Haile: They don't care about everything and the DAP itself is only interested in a small little segment of the all blockchain because it's adapt, it's an specific user interface and so having an memory sync mechanism was very helpful.
Deniz Mert Edincik: Yeah, it's actually very good idea. Not like what I am targeting for. The tiny aien is long compute, but High disk High storage. So it will index it will have historical it will have. all the bells and whistles and it will just act like access notes.
Tom Haile: Yeah, yeah. So we did a version of that around 2018 where we had a node app that would essentially have a poster database and it'd be a service that would do all the sinking on your machine. And then the DAP would sit on top of that and then later versions we move that kind of node thing into the web browser itself. So it was all self-contained. And it worked. I mean it was fine and
Deniz Mert Edincik: Yeah, it's pretty good. it's very tiny terms of usage it's like I am running on five dollar VPS So he isn't some requirements.
Tom Haile: Yeah.
Tom Haile: nice. Yeah. Yeah. But I think what Ali wants to get to is more of a generic data availability architecture.
Ali Serag: Yes, And I want something as stupid simple as possible. Someone comes into the ecosystem. They're just learning about flow. They want to do an airdrop or maybe they're not super technical. how do I get access to API endpoint so that I could get the data that I need or build an application that I want to maybe because on ethereum a huge amount of the developers aren't actually solidity devs. They'll forkenstein solidity contracts, they'll deploy but they're front-end debts. they build nice ui's and they just look everything up. So for those types of developers,…
00:50:00
Deniz Mert Edincik: something like yeah,…
Ali Serag: we haven't really catered to them.
Deniz Mert Edincik: it's like some rest API like I can share with you I had this from this tiny and…
Ali Serag: exactly
Deniz Mert Edincik: Something like this, for example.
Ali Serag: who? Yes, yes exactly like this. All right, next working group. You're gonna presentation. It's not going to go deeper into
Deniz Mert Edincik: yeah, I just did on the weekend, it's like I need to index more…
Ali Serag: wow. then
Deniz Mert Edincik: but it live. For example, if you refresh that address if they send some transactions spend some love. You should see.
Ali Serag: Yeah. Wait,…
Deniz Mert Edincik: Or something like this.
Tom Haile: Circle
Ali Serag: what inspired you to make this again?
Ali Serag: really? I love this.
Deniz Mert Edincik: It was like your ideas. I was thinking long time to Make storage indexer but on the Cadence side,…
Ali Serag: Yeah.
Deniz Mert Edincik: it was like little tricky. Now it is much better.
Ali Serag: This is awesome. this is really awesome.
Ali Serag: One thing I know we have one minute left. I want to plant in everyone's mind is thinking about data access and availability on and EDM side so I'm not so sure how many people here have experience with developing on evm. But thinking about what would be your favorite tool to be able to query data. Would it be the graph would it be Morales? Would it be Alchemy would it be covalent? And what would you love to see on dbm side just gonna plug that in there because we're at time. But thank you guys so much. This has been super helpful and especially Jack Dennis like you guys have been awesome.
Tom Haile: I would say all they also snapshot into your bucket and…
Deniz Mert Edincik: Thank you.
Tom Haile: even on the inside as well. Yeah, it's a snapshot of users token balances to give them voting power.
Ali Serag: snapshot in terms of voting on chain voting
Ali Serag: Interest I never thought of it that way.
Tom Haile: Yeah, so instead with snapshot you just basically write a query, and then you have all these queries that get chained together in order to give the users voting power for various proposal. However, it's organizes like that so can be all sorts of stuff. They can get really complicated.
Ali Serag: awesome Thank you guys so much.
Tom Haile: Thanks guys. Thanks Ali.
Deniz Mert Edincik: Thank you.
Ali Serag: Bye.
Meeting ended after 00:53:44 👋

