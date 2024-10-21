Dev Tools Working Group (2024-08-01 10:07 GMT-5) - Transcript
Attendees
Alexandr Ni, Ali Serag, BoHao Tang, BoHao Tang's Presentation, Brian Fisch, Chase Fleming, Diego Fornalha, Giovanni Sanchez, Jack Forgash, Jordan Ribbink, read.ai meeting notes, Tom Haile, Tom Haile's Presentation
Transcript
This editable transcript was computer generated and might contain errors. People can also change the text after it was created.
Ali Serag: About documentation Etc here. we're thinking a lot about tooling that is relevant For Crescendo, and one thing that I really wanted to talk about because we're thinking about doing things in themes focusing the theme of this month overall being gone nfts, and we have a stellar Gathering here. So with Jack present I'd recommend if we could to the agenda talking a little bit about data access in the ecosystem and the the documentation that we've been putting together and the second thing I'd recommend adding if possible is talking about nft catalog and the future of that. Yeah, that's pretty much it on my end. Let me know if you guys have any questions. Sorry, my morning coffee hasn't kicked in yet.
Tom Haile: right I thought we were getting rid of entity Carolina. tell me why we're not getting rid of it.
Ali Serag: We are …
Tom Haile: okay, okay.
Ali Serag: but we should discuss what we're replacing it would.
Tom Haile: Bob what you got?
BoHao Tang: Yeah thinking about unless you catalog. So a question is if we process after the creation upgrade. I think there are maybe not several lots of nft. be broken on catalog. So directly and if the control is okay the catalog it upgrade the code in the rainbow. But yeah, we query something in cats all that will be through some error the transaction may be failed. So any idea of that things? I don't think
BoHao Tang: A lot you will be upgrade after creation notes, but with several app floor wallet and maybe other Place directly using you have to catalog to query the information. So I'm not sure. Because I have a plan to upgrade my token list to to do anything else brief requiring to get rid of some vulnerable token in my token list and I live as a function to avoid That kind of broken vulnerable console wise that obvious then problem.
Tom Haile: And how are you updating your token list? Do you read events?
BoHao Tang: My plan is to add some new function and remove sound like broken vulnerable token. That's my idea. And after that upgrade I will try out to fix thats discard that it didn't happen right now, but I can't set up on my fitness platform. I can create some token not upgrade and some close upgrade so I buy some functioning of finds our way to to remove the broken portable. But yeah if we do anything on and Lefty catalog that will be caused some issues when adapt or water directly using Electric Catalog and maybe query for all then boom.
BoHao Tang: The description will be gone. So
Ali Serag: so an ft catalogs already been upgraded for Cadence one point so I believe me.
BoHao Tang: Yeah, but the unity record in the left catalog. They are probably some broken nappy. that yeah.
Ali Serag: All right.
BoHao Tang: So that's what problem.
Ali Serag: so I guess does it make sense the kind of try to audit all is there Surfer interjecting?
Tom Haile: It's good to know. I guess.
BoHao Tang: I don't think that's all this thing. we want to avoid that kind of broken up you win as a function and remove them from the list.
Ali Serag: We need to remove them from okay, if they're away that we could gauge how many of them will break due to not upgrading.
BoHao Tang: and not deal
Ali Serag: could we just see which contracts are listed on NFC catalog and see on Dennis's tool which of them have been upgraded which of them haven't and then reach out to? we map the owners to be And get it 30% of these assets are going to stop working and then come up with a way to remove them. Or either get the people help support them to pay for a certified Cadence experts to upgrade them. But if we can't get a hold of them at all and they end up breaking then just remove them are minus misunderstanding.
00:05:00
Tom Haile: Maybe Gia's got something.
Giovanni Sanchez: Yeah, yes. I just want to interrupt thread. This is taking it a potential solution. So This feature proposed for ce specifically performable tokens where if a contract isn't updated to a Cadence 1.0 you can still access. I think the type that some of the fields. that might be helpful for this use case. So that's another thing we might be able to do is talk to the Cadence and see how feasible it would be to include nfts and not as well.
Giovanni Sanchez: At this point I don't know. We're cutting it pretty close, but
Ali Serag: Are you working closely with the team on that? I remember proposed it. But do you think you could follow up with the team Geo to see if it would be too short for them to add nfts?
Giovanni Sanchez: yeah, I'll go ahead and follow up with cadence. I think passion and Josh we're working on it, but I can kind of act as go between
Ali Serag: Because if we are able to maintain that data and ensure that nft catalog doesn't break with those assets then that fixes or resolves that problem. If not, then I think you could just audit which contracts are likely going to try to reach out to them to upgrade them and give them support to upgrade them. And then remove them from catalog after they break.
BoHao Tang: yeah, I'm afraid we really hard to like fun. Everyone who have beyond that. Maybe they just give up at I don't know so I don't even find a way to after the upgrade.
BoHao Tang: At least in short term. leather the Lefty catalog. Didn't through any error that maybe we need Focus solution for that. But when we have the upgrades after that upgrade, maybe we Can discuss those solution? I don't know.
Ali Serag: okay, but I like the path of using token list and fixes as a way to go on.
BoHao Tang: Yeah, Token Focus. Yes, since I count their students and token it so I can find a way as a function and some script to scan all existing token on tokenist and they're check if this rainbow and do maintain so it's okay for upgrades, but I'm not wore.
Ali Serag: that's
BoHao Tang: I'm up right there. Yeah, a lot of people project didn't care about the upgrade and maybe just give up so.
Ali Serag: Okay, so it sounds like the plan then is all right. Leave nft catalog as it is for now. Make sure that it's maintained make sure that the assets on it don't cause any breaking issues make sure that it's upgraded to can point. which you've already done but start after Creator goes live on testnet. Building an alternative you like in a deep centralized way that we don't have to rely on maintained catalog anymore with token list and start transitioning everything over to token less and start talking to the market places to start pulling data and working directly with token list instead of catalog and…
BoHao Tang: Yeah. Yeah about coconut.
Ali Serag: slowly Sunset catalog.
BoHao Tang: I think we are well met another problem is some since it's a permissionless or anyone can register adding things on the complex. So maybe we need some verification process for that but I'll be using coconuts another question.
Tom Haile: You the question when you say token list,…
BoHao Tang: But yeah not
Ali Serag: Yeah.
Tom Haile: I'm not familiar with that. What is tokenless?
Ali Serag: Could you do a screenshare and share and maybe it makes sense? for those that familiar with cattle?
BoHao Tang: okay. yeah. let me screen.
Ali Serag: What are the problems with catalog? Why do we need to change away from nft catalog? what value does something like token less to offer as an alternative?
00:10:00
BoHao Tang: This is totalist.
Tom Haile: So token list is a name of a product. our website I got you.
BoHao Tang: Yeah, okay, okay. That's the Poconos.
Tom Haile: Okay makes sense.
BoHao Tang: So if you want to like here is a old phone here.
BoHao Tang: And where you want to Register phone, it's really easy here is you're just sorry. Let me copy the address.
Ali Serag: think
BoHao Tang: Yeah, just read it. And that's all so yeah, when a well affordable token deployed to a address and just input address there. I will like query old bottles under this address and if I don't not registered you can rest to the vulnerable and then you are fine.
BoHao Tang: There's all this data inquiry on Chen and Drug required on transle is a view for Did Jason file in place on the unit's web tokenless standard old onion. Sorry notes of talking lists used by uniswap and a lot of other debts using these So I'm using coconut token list standard to do this project and…
Ali Serag: And The Real Slim Shady,…
BoHao Tang: all data is right around Chan and…
Ali Serag: please stand up.
BoHao Tang: I use API to decorate old for both and register for token and generate this program list Jason file and also provides down the script to directly loading that and yes, actually we can like using
BoHao Tang: a very fear to add to care with some features and verified. So the problem of maybe a fake fundable token. We send C us here. This is a real USBC and some guys create a fake USBC here. I think where is the favor Justice? I think there will be a great uses equation.
BoHao Tang: Yeah, this is a real one is the object token. And another is quote on fix this Wars. And yeah, this is a fake one. Because it is a fake one. But yeah, the uses then image but I can set out is a feature. So if incredible fire using the detail pad here from tags in the Json file, if you use that can be okay for I didn't hear which token verifies yeah, but it seems like I didn't do that other whatever I just told them if they want to use they can use it and this is done. This is the API and point for project and this is Crips for that. simple and there I have a little website for test notes.
BoHao Tang: post notes you This little test notes.
BoHao Tang: Yeah, it's important. And then sensing like I would a lot of my icon.
Ali Serag: I'm here.
BoHao Tang: So whatever just using that protest that testing and yeah.
Giovanni Sanchez: Yeah. Yeah, this is great. I mean it looks awesome. The issue of impersonations. I don't know that's like something we could really solve…
BoHao Tang: Bro token on test that to…
Giovanni Sanchez: but thank you probably saw that as best as we can as have verified I think.
00:15:00
BoHao Tang: but Cadence 1.0 and…
Giovanni Sanchez: I've seen that on Phantom wallet when you're interacting with the Texas have verified contracts.
BoHao Tang: the last song is still broken and I will try to let the phone talking lists…
Giovanni Sanchez: So I think that's probably as good as we can.
BoHao Tang: what after the Christian not great.
Giovanni Sanchez: get to
BoHao Tang: And that's my plan to upgrade toklift.
Ali Serag: So who would again the reason we created nft catalog is the same reason token that's were created many years ago on another ecosystems…
BoHao Tang: So I found out maybe. Lefty catalog well met several issues of the upgrade a lot of Unity on the phone of Chicago is not upgrade.
Ali Serag: which is to make sure that there's no fraud duplicates, make sure that the tokens are legitimate Etc and as inclusive transparent and…
Ali Serag: decentralized way as possible and we shared the links in the chat around those so token let's make a lot of sense…
BoHao Tang: Yeah, I can give the link post here.
BoHao Tang: Jill.
Ali Serag: but to your point, it's impossible we want to move away from centralization. But as long as you have a verification mechanism you are creating Gatekeepers in one way shape or form. How do you guys think we can affectively as decentralized as possible create a verification process and who would those verifiers could it be anyone in the community? Would there have to be specific people like the marketplaces? Yeah curious to your thoughts.
Tom Haile: Chase's got some
Ali Serag: mmm
Tom Haile: Yeah, I would.
Tom Haile: Yeah, my thinking is it's like a verification of a fungible token is kind of a multi-step thing. So where's the liquidity? What pool is it in? And that gives you an idea about if it's going to be valid or not. it's that kind of thing. But ultimately, you go to come coin gecko you go to these various places to look at the liquidity and all that kind of stuff to see it's the actual real token or whenever you get an airdrop you go look it up and you'll be like, this is a real thing or not. and it's kind of
Tom Haile: Yeah, I'm wondering as a topic of discussion. How do you go verify something on another change? how do you go verify if you want to go buy a particular token because Meme coin or whatever. Where do you go to make sure you have the right contract address so that you can go and buy it wherever decks that's kind of a question. I think Giovanni's end up first.
Tom Haile: Think about I think Ali and then bohao.
Ali Serag: I mean the naive implementation that came to mind initially was like okay, if you have two conflicting names, can you just look on chain? What is the first contract that was deployed? And that's most likely to be the original but then looking at the mean coin world as soon as they're speculation that one celebrity or influencer is gonna launch it's open people months before they want to token try to create fake ones. So time alone isn't good enough. I like the idea potentially exploring metadata views for nfts and having because right now to Geo's points, if I am following and influencer someone that's going to launch a new meme coin. I'm waiting for them to post the contact Azure the contract address. And as soon as they do that, I know that that's the original if I go on the meme coin website, I verify the contract address.
00:20:00
Ali Serag: it would be interesting potentially. I don't know if it's a terrible idea to
Ali Serag: Maybe one field in the metadata could be the link to the Tweet where the Twitter account of that organization posts the contract address. So people could directly go and see and verify from the UI because you're pulling and showing that a little Twitter icon or…
BoHao Tang: Alright, I dropped twice.
Ali Serag: something you click on that you directly see …
BoHao Tang: So I do something I forgot to tell you about the tokenist and…
Ali Serag: yeah. this is the Tweet by two cans or…
BoHao Tang: here is a strategy I try to let the verification process and…
Ali Serag: this is cheap. I blah blah, and maybe we could even add a Twitter authentication process to verify that they are the owners of those accounts and…
BoHao Tang: I create editor for the talking list.
Ali Serag: they did make that Twitter.
BoHao Tang: And that is everyone and…
Ali Serag: I don't know we could get creative in that.
BoHao Tang: everyone can be a verifier, or maybe I can call the reviewer.
Ali Serag: o o o
BoHao Tang: so if you like Logging here. You can maintain coconut View and…
Ali Serag: o o o
BoHao Tang: here you can set
BoHao Tang: a review like verified using this feature and…
Ali Serag: o
BoHao Tang: you can set you updated token review as a feature or verified and I can using and choose a token and…
Ali Serag: o
BoHao Tang: set a verified here and then here any reviewer can be in here. You can select the reviewer.
BoHao Tang: Check here if you select the reviewer to query the API or Acquire The Script, then you will find the tag rev verified then if you didn't using that there are no ending text here as empty. So anyone I mean adapt your owner or something probably create whatever wallet or that using these platform. You can review by yourself.
BoHao Tang: By yourself and you can think we kind of token you want to that verify Tech. This is my Nick. I'm setting sound like some token is verified and there's something like that but if you want to for example increment buy income of my credit their own reviewer accounts and using these three review accounts that several token that's verifies. So I think that's my strategy for the total is to verify a token. So everyone can be a reviewer everyone can choose their own verified tokens. Reviewer can be anyone reveal. If you are that owner. You can be a reviewer and the API you're using just set the reviewer as your resource.
BoHao Tang: 
BoHao Tang: Sorry as your address.
BoHao Tang: Yeah, that's my idea.
Ali Serag: But what?
BoHao Tang: So I just query this address with my review the token that can be only my Revival token in here song that parameter. I just…
BoHao Tang: 
Ali Serag: What prevents gaming of that bohao what if I just make a scam token and just verify it?
BoHao Tang: He had the future that parametera.
Ali Serag: Yeah.
BoHao Tang: So if you choosing future only my review the token can be list on The Talk list,…
Ali Serag: Okay.
BoHao Tang: then you can only get that kind of tokens. So yeah, just my strategy about her how to reveal token. Give a game give everyone can be a reviewer to rebuild our Vital control. And yeah, you just choose the soup but your own source.
Tom Haile: there's other ways of kind of verifying I think it was like that screener. I think that's what it is. that right deck screener where It can give you a health of a token. So basically since ERC 20 tokens are pretty standard contracts that it can go through and say, is there a pre-mint is there trained transfer fee, what are all the chances that it could be rugged all that? Okay, is there all sorts of different kind of metrics and it's based on my understanding is in space on consuming the actual contract in order to give token holders or people that want to trade it better confidence?
00:25:00
Tom Haile: of that particular C 20 and it seems like that would really only be the actual way that you can build some Trust. the Ali
Ali Serag: I find this very interesting. What if we just did merge authentication using Twitter sign in people's Twitter accounts and you could literally see this was their reviewer. This is their Twitter account if I see Jacob Tucker's Twitter account and he's the reviewer of xoic I have high trust for that. But then if I see a rando because first of all, it makes it harder because people are gonna dox themselves as reviewers and I don't see why that should be a problem necessarily.
Ali Serag: but it adds a extra layer of trust and also adds an extra layer of difficulty to gain in my opinion. And I know that you're working on using Twitter verification for some other stuff related to fix it. So it might be an easy lift. But I'm not sure if it pulls it but I think it's a very interesting path.
Ali Serag: I think Chase.
Chase Fleming: was the verification security stuff not like the original purpose of clicks can you do that with the contract already…
Ali Serag: Yeah.
Chase Fleming: because it's like I don't know Tom could speak on that ignoring the scripts and transactions and stuff is there. a way to use that. Because it's audited already.
Tom Haile: It's true.
Tom Haile: Yeah for flex and stuff on the Cadence side. it is possible for it to get audited and that's just auditing the transactions and of course contracts that have to be audited. But there's no where to go. Look for what contracts have been audited unless you the auditor and maybe they advertise it or something like that. But yeah can be audited.
Chase Fleming: But token lists show audited by flicks or something. if it's flicks audited tokenless could be like that one's not acts as a form of verification or something.
Tom Haile: Yeah it would have to go find The Flicks and then associate contractor dresses, the import for contact contract address in The Flicks to match it up with the actual token.
Chase Fleming: I mean, I guess could you just put the link to it in the pragma or something and then run something to see if the hash of the contract matches that what's the link or the one on the pragma? And because you were able to add it to the contract? Thank you approved that Netflix.
Tom Haile: so you're saying in the transaction and have a hash of the contract and that will verify the Contract through the flicks all that's already there as well. So yeah, it's
Chase Fleming: I mean I guess put a link to the flicks and the contract or something. So a comment. I don't have to think about this so that on tokenless you can look at the link pull it hash it against what you're using and then yeah that matches or something that's verified. I don't know. I feel like there's something there with being able to put a link in that pragmire in a comment or something.
Tom Haile: yeah, you'd have to know all your transactions. By the time that you deploy your contract. and the hashes we would have to match in order to the Truly. Trust it.
Chase Fleming: What do you have to know the transactions or do you just have to know the original contract? To know that that one was verified. there
Tom Haile: it depends so the flex has a hash of the contract. And so you can verify that this transaction is for this particular version of the contract and I don't know if we're getting rid of upgrade ability. Are we getting rid of up variability or is that still gonna be a thing in case 10?
Giovanni Sanchez: That'll still be a thing. I think we'll just encourage people to once they're stable to revoke keys.
Tom Haile: So if there's an audit of the transaction and transaction has a hash to the contract there is kind of a train of a chain of trust there.
00:30:00
Tom Haile: And yeah, I mean, so to your point Chase, Yes. you can verify the hash of the contract in the flick.
Tom Haile: And here Let I just want to show the Dex deck screener right quick to kind of finish up that point of an audit. let me see where.
Tom Haile: Yeah, so here on Deck screener. it has
Tom Haile: this part over here to Ryan middle. It's kind of busy. It has one issue. So this is just some random token that I read but it has all these different metrics based on the contract code. And so it gives your the er The creation address, all that kind of stuff is it mental? No and here it has a finding so it has a black list. So they consider that a finding. And then is there a bike tax? No cell tax. all that kind of stuff. Can you change the tax? It's a transfer tax that kind of stuff. And so someone that's jumping into these random coins as thumb degree of confidence that they're not going to get rug instantly that kind of thing.
Tom Haile: I just wanted to Let's describe another one. I don't know. there's another one. So this one has a finding as well. Okay this one has a white list. Anyway, so this is kind of interesting. And this is just on a theorem stuff. Here's
Ali Serag: Use lists sound like centralization. What is this?
Tom Haile: Yeah, banana has a bunch of findings. the ownership as a tax But It's not an all, but I'm just saying profiling the contract at least gives users something to look at,
Tom Haile: and I'm not sure if that's even possible on the Canadian side. Maybe after Crescendo where we had a more standardized functional token.
Ali Serag: Okay, because just being cognizant of the time, but I want to tie this all together. So In terms of tutus Geo will see if there's a potential work around for the assets similar to what's being done for comfortable tokens reason we need this is because the non-upgraded nfts will break on NFC catalog which will have a ripple effect on marketplaces that ingest them if that isn't something that's possible. What would our plan be because we have two weeks. You should. you're muted Tom.
Tom Haile: I know I'm just saying two weeks. Yeah. Good,…
Ali Serag: three weeks
Tom Haile: let's get there.
Ali Serag: Anyone have the ideas on what the best alternative plan? Our course of action could be.
Ali Serag: For those assets that are breaking on catalog.
Giovanni Sanchez: I guess maybe the plan that you had brought up originally…
Tom Haile: ignore
Giovanni Sanchez: which was to see which. out of all the nft contracts that are currently in the catalog which are failing migration which aren't currently staged or failing migration and then remove them from the nft catalog.
Giovanni Sanchez: And then also I guess my question would be in the worst case where we do nothing. What does that do to the contract? Does that mean the entire mapping of types breaks or just encountering the broken type?
Giovanni Sanchez: So kind of like scoping out what that would look like because I did see that in the flip. It's scope to support nfts at some point post 1.0. but I don't know how realistic it is to get that ready by migration.
Ali Serag: On a team would be the best who did for investigating the mappings and what would happen.
Giovanni Sanchez: I mean, that's something that would probably be within my wheelhouse but right now I'm not sure if I'll be able to add that to my scope for them.
Ali Serag: anyone else that might be suitable.
Giovanni Sanchez: Josh or I mean anyone here if there's anyone who would be willing to check that out?
00:35:00
Giovanni Sanchez: but as a starting point I can.
Ali Serag: any volunteers
Giovanni Sanchez: I can follow up on the flip and see how realistic it would be to add kind of nfts for planning.
Ali Serag: All right, let's take that approach. And then I like those three options then the second thing is Bohao, are you good to continue investigating potential enhancements to the verification process or tokenless the NFC version of token lists.
BoHao Tang: yeah, definitely an optimist It works when my plan is after upgrade to presentation and I thought I have some negation for the life to the new talk list. Yeah, since I think the Warby using some mechanism front tokenist performance of it just a copy for the mass structure and…
Ali Serag: Yes.
BoHao Tang: do the Product similar products for lucky there will be easy and they're still using the standard for the Union's web tokenless tender than the building something. This should be quickly one week. Maybe I can build a prototype for that. But my plan is after upgrades Then I…
Ali Serag: so that transitions nicely to the next point this next working group will be a day after Crescendo on testnet.
BoHao Tang: then starts through the migration. So we'll be better.
Ali Serag: So I think it's a good topic to continue going into the next one.
BoHao Tang: Yeah, yeah.
BoHao Tang: Yeah, since I don't want to waste of time on the broken Lefty maybe a lot of Brokenness young.
Ali Serag: Yeah.
BoHao Tang: I just find some way to ensure all the volume. another bottle open on the new tokenness is working and then I can start Being a similar products like the token list and through also maybe I do have more editor about the the verification process for focuses a decentralized way and verify the reviewer can be anyone so if you very trusted the reviewer, then you can trust this. total as it is verifies, so Just I think that's the easiest way to do that.
Ali Serag: That makes sense. I did have a quick question. I noticed that the flow All Hands was gonna conflict with the developer office hours. Does anyone have any contacts into if we're still doing the developer office hours or
Ali Serag: A little bit of a tangent. I'll ask on Discord. It's probably a better place. Thank you guys so much. This was a really valuable discussion about nft catalog and I think we have a pretty clear next steps for it Tom. I'll hand it back to you.
Tom Haile: I was hoping that Jill give us a little update on the bridge. I know you made some minor changes and stuff. We can kind of transition to EDM stuff.
Giovanni Sanchez: Yeah.
Giovanni Sanchez: Yeah on the bridge there were some changes following the audit just some things mostly Strengthening guarantees, especially for end users adding conditions and assertions within the transactions. Those changes There were some that were breaking that wouldn't be compatible updates. So, pretty not being a test Network a redeployed those contracts yesterday. it sounds like they haven't been integrated into flow Port which is kind of like the staging environment for evm on preview net and cross PM transactions using the bridge.
Giovanni Sanchez: But yeah, so that was deployed getting things ready. I mean in terms of coming migration for testnet getting things ready for deployment there. It sounds like there's some things that might be changing with pretty minor and nothing that's core to the basic functionality of the bridge just kind of like ordinary and sequencing based on whatever kind of ends up settling down out of the circle conversation, but I think there will be announcements about that soon that will direct what changes I need to make to the bridge repo but Prem unit soon to be integrated. It sounds like Tom and Alex will be working on integrating that new deployment of a bridge on pre-unet here early next week and internet and so the end of next week so That I expect that should go smoothly. So kind of
00:40:00
Giovanni Sanchez: in a holding pattern right now for the bridge until test not migration and then that will be deployed there. shortly after
Tom Haile: Right, right. Very cool. Yeah, we need to make distinctions when we start talking about crossing bridge that kind of stuff and…
Giovanni Sanchez: right
Tom Haile: Alex. Do you have anything you want to say about that effort and the flow Port stuff or the preview net?
Tom Haile: Okay, So that'll be on preview net so we can get ready for testnet, a lot of Lonnie Lottie. That'll be good and then talking about bridges. I'm working on the bridge on top of axillar. So that'll give users the ability to move. Axlr wrap tokens to the evm side on Flow. So it looks like we're going to be targeting essentially three. So reppy threat Bitcoin and axillary usdc and so that'll be able to help users outside of the ecosystem get into the ecosystem on the udm side. And so that'll be coming and be available day one. when maintenance available after the crescendo?
Tom Haile: that's kind of a kind of fun all about bridging right so we gotta allow liquidity to come in and move around all that kind of stuff kind of reminds me of If you remember way back in the day and PayPal, so PayPal made a decision early on to allow people to move funds in and out of there ecosystem. Because users that know that they can move in and out have a tendency to stay in the ecosystem. so therefore, convenience is very important for users. So they have a sense of not being stopped being able to move around in and out of ecosystems. So looking forward to that day one. May not gonna be a lot of fun. But that's kind of the bridge stuff. any other
Tom Haile: I got any other evm tools. Anybody wants to talk about are any tools missing in the ecosystem.
Ali Serag: What about a couple of things we talked about last working group were the nft faucet and we're SDK.
Tom Haile: The cross VM nft is that we're talking about. bridging
Ali Serag: Yeah.
Tom Haile: Up, Jim you had something about that.
Giovanni Sanchez: No, actually it was something else.
Tom Haile: Yeah, Go ahead. Joe wouldn't come back.
Giovanni Sanchez: yeah, yeah, so I guess. two things so one being especially with the presentation that bohao kind of walked us through of Texas this idea of a token Factory on Cadence, I think two cans kind of serves that end. It sounds like fixes kind of serves that end, but that's in Cadence. And I could see someone coming to flow and flow evm and maybe wanting to be able to deploy to either one.
Giovanni Sanchez: So I guess that that would be kind of interesting. Right so you go to fixes and you could deploy to either evm report a Cadence and do either one just as easily. the other thing sorry, I'm getting a couple ideas at once. So I guess I'll just stick with that one.
Tom Haile: No, no keep him coming. But okay Mom you have something to respond.
BoHao Tang: Yeah, that's a question. I think I'm not really familiar with current I'll blow and the Bridge So if I want to deploy a strategy bridgeable affordable token,…
Tom Haile: cool
BoHao Tang: I have deploy.
BoHao Tang: A solid he contracts our evm environment and the religious something on our VM Bridge. There is any documents about that if I can make their fixes as example to write really easy to create a breachable token and for maybe showcase, I'm not sure but country. I want to know about how to create a burgeable token on both sides. Okay? Yeah. I don't think That's automatically, maybe we need deploy sound sounds that's good contract and…
00:45:00
Tom Haile: right
BoHao Tang: read something and there are document about that or anything about that,…
Giovanni Sanchez: Yeah.
Tom Haile: Let's get question.
BoHao Tang: or maybe you can tell me something about that. I can write some example and rise up document. S and I also like quotes on the fixes.
Giovanni Sanchez: Yeah, I mean, that would be great. Yes. Go ahead, Tom.
Tom Haile: there's A two levels to that. Right? So I think what G was going to talk about on the contract level. I assume you're gonna talk about that where you could go get transactions and all that kind of stuff and then just call contract specifically to bridge to cross VM bridge, then there's flow Port. So there's some button clicking that you can do to bridge either from the Canadian side to EDM side or from the inside to the Cadence side. If you already have an existing fungible token or NFC token,
BoHao Tang: Yeah, I mean my question is if there is since ending existing vulnerable token contract. I want to create some meme coin that is a bridge bowl mean coin. So I want to create an example or maybe great. Yeah, it's not showcase about how to create Bridge ball token probably on evm side and locate in size. So I want to know the person and instructions that
Giovanni Sanchez: Yeah, nothing super in depth. The readme on the bridge is probably about as much documentation as there is I think I have some design docs that I would like to Work up. I just ended up getting put on another project immediately after the audit for the bridge.
Tom Haile: right
BoHao Tang: again
Giovanni Sanchez: But I think that There's across VM kind of bridgeable implementation of a fungible token and then from there, I mean you tapping into the liquidity on either side than interesting defi strategies, right rebalancing across VM Arbitrage like things like that. I thought would be really cool to explore. and even just deploying an evm contract from Cadence alone would be really interesting. So I would love to talk more and we're approaching the end of time, but I think this is probably something that be worth kind of exploring.
BoHao Tang: Yeah, So every transaction is the problem okay to the side and deploy a bridge ball. It's already contract and they're in England Cadence My Control, right?
Giovanni Sanchez: Yeah, yeah, so I guess there's a couple of ways that you could do it.
BoHao Tang: Okay.
Giovanni Sanchez: You could deploy a factory contract and solidity and make calls to that contract from Cadence and…
BoHao Tang: Okay.
Giovanni Sanchez: make COA an owner.
BoHao Tang: God did God.
Giovanni Sanchez: Yeah. Yeah.
Tom Haile: Yeah Ali.
Tom Haile: That's funny.
BoHao Tang: Yeah. But whatever.
Tom Haile: it's the Paradigm of selling shovels, right and the gold rush and you need a gold rush first right in order to sell shovels. That's kind of the thing but The Boathouse so for deploying evm contracts, there's a web UI called remix. I put a link in here.
BoHao Tang: Yeah, yeah, I know…
Tom Haile: We have it to draw.
BoHao Tang: what? Yeah. I know that's what I mean is not using that kind of traditional Tours to deploy EDM contract, I mean is popped on Farm just let user quickly click something and three Creek maybe and…
00:50:00
Tom Haile: right
BoHao Tang: deploy a new phone that of fixing word already have these poker launcher service. any user
BoHao Tang: But what I want is improve that and every token notes on fix this can be a bridgeable token. So that means I need to deploy a contract not only the Cadence contract but also we need a way to deploy a templates like Bridge ball yet in 20 contract on Flow evm so that I want to know more about the details and…
Tom Haile: yeah, so 80 token that conforms to the metadata standard can be bridged.
Giovanni Sanchez: Yet.
Tom Haile: Is that where you're gonna say Jim?
Giovanni Sanchez: Yeah. Yeah anyone so if in the context that fixes you have a Cadence fundable token you just on board that to the bridge and…
BoHao Tang: maybe I can write on documents and…
Giovanni Sanchez: the bridge deploys a corresponding erc20 and…
BoHao Tang: and write something to tell developer.
Giovanni Sanchez: just basically connects the wires between the two of them and…
BoHao Tang: Yeah, fixed the easy way to lock it,…
Giovanni Sanchez: vice versa the other way around you start with any RC 20 deploys a Cadence contract in Cadence.
BoHao Tang: but other development you want to learn more about how to deploy a verbal token both side, so
Giovanni Sanchez: So really you just need to deploy one contract you could make it Cadence or evm native and I guess it from flow foundations perspective probably would want to support Cadence native and then onboard that to the bridge and users will be able to move between the two
BoHao Tang: Yeah, I have enough questions. So is it possible we like just one transaction to deploy two contracts possible on Impossible?
Giovanni Sanchez: So it's possible going from Cadence to EDM. So if you deploy Cadence transaction and you onboard to the bridge, you could do that in a single transaction. You'll have erc20 and Cadence fungible token all in one. Other way around you you would have to do in two transactions.
BoHao Tang: Okay, cool.
Giovanni Sanchez: Actually that true. No, I think that would actually work as long as you're not trying to bridge in the same transaction you could do two in one in either direction.
BoHao Tang: cool
Tom Haile: I think that's all the time. We have I appreciate everybody. participating engagement and yeah, there's definitely
Tom Haile: Definitely requests for documentation, So that makes complete set. So when we get flow port on testnet when there's testnet upgrade that'll help us solidify more of the user stories and stuff like that for flow port for bridging and then we can build out all the documentation and stuff, already has all the documentation bridging for the contracts and stuff. There I can post post that link.
Tom Haile: lots of great documentation to the Fuller Union Bridge. Thank you very much Geo. or Writing all that up. I mean it's really really comprehensive. Yeah.
Giovanni Sanchez: I'm glad to hear that because I was worried that I didn't have enough time to make a throw enough docs. So if you do have any suggestions, that would be Great, but glad to hear that. It's helpful.
Tom Haile: Yeah, excellent. So anybody have anything else or we were done?
Tom Haile: All right. Thank you very much guys.
Giovanni Sanchez: until take
Ali Serag: Thank you so much. Bye.
BoHao Tang: Thank you. Bye.
Alexandr Ni: You guys here?
Meeting ended after 00:56:34 👋

