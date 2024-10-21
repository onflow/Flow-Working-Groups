-- Transcribed by TurboScribe.ai. 

Today I'm going to talk about the compatible address that just deployed, so maybe have some bugs. Let me check if there are any bugs here. Yes, still some issues.

I need more debug. What the hell is it? Whatever. It works fine, kind of looks like fine for now. 

And you see here it's just a bridge attack. That means this NFT is already bridged to the event. Still some bugs.

I need more debug, but yes, the result is EVM, any EVM address and the flow address, just input here and you can write an address there. And you can get information for that. And if you input, let me check if there are any, whatever. 

It seems like this is a bridge. EVM address here. If you input EVM address, there are query from here.

It's not registered, but it's a bridge and you can register these assets to the token list. There should be only one input box and then just register the EVM address. Then you can directly onboarding assets.

If there is an asset not without bridge, for example, let me find this one. It's my coin. This one, you can onboard into the EVM bridge. 

I'm not sure. In the testnet, I just onboarded to the EVM bridge across the workflow. I just put the information there, but let me check.

If you like any vulnerable token or non-vulnerable token, you can find in this Slack box. And if it is not onboarding to the EVM bridge, there are still some bugs. What the fuck? Maybe I'm missing some dependency address. 

I will fix it later. I think the testnet version works well. Because the mainnet version, I didn't fully test it.

Just deployed just now. Check this one. Address here.

It's not bridged to the EVM bridge. Switch to testnet and onboarding it. When I finish the transaction, the new RCDR is a bridge 10.

I think that's all updates. I will check. I think that will be as bridged now.

You can check only all of the bridged coins here. This is a JSON view. That's all.

It's fully EVM compatible. Including EVM list now for non-vulnerable as well. For EVM only, just listing all the bridged tokens.

Just updates on how to use here. How to use here. If you're using vulnerable token, non-vulnerable token and tokenless, if you want to query EVM only, just change some scripts.

Here is the cadence scripts if you want to directly using the cadence. Here is the cadence sample. All the things here.

Welcome to use it. The bugs are only on the EVM side. I think there are several dependencies I'm missing.

I will fix it. Mainnet version will be worked for today. This looks awesome.

I love that you can see tokens across EVM and cadence. If I were to deploy a new token, whether it's through Toucans or their own project, how is it picked up by the token list? You can just input the address in the token list and register it. Anyone can do it.

If you want to directly call a transaction inside your transaction, it's just a one-line code to include it into the token list. Let me share it. I see. 

I would have to deploy and register for it to be picked up by the token list. Yeah. For the registration, this is the two transactions I used for the registration.

You don't need to onboard to VM bridge just using this single line. For the Foundable Token, just ensure Foundable Token registered and the input address and the contract name. For NFT, like this one, one-line code.

You can directly onboard to the token list. But in this method, there will be check. For example, in the token list, ensure this is valid to register this method.

I'm checking all the view reservoir and only check these two connections. Sorry, this metadata view. If it is valid, then register. 

Without this metadata view, it didn't register to the list. Simple. I have a question.

I have a question for the VM bridge. The problem now is check this one. All the bridge from EVM, if the Foundable Token bridge from EVM, or maybe the NFT bridge from EVM, the icon is the same.

It's like this row. This one, I'm using the editor inside the token list. For this one, I just added it to the ESVC. 

But for any token from the VM bridge, without editor, it will be the same icon. I think this is the problem for now. It's only a problem for the VM bridge token.

From Flow to EVM, there's no problem because there's a view here and we can see a different icon there. But for tokens from EVM, there will be an icon problem. I don't know how to solve it for now.

Hal told me that we can use a GitHub repo to connect to a logo. But yes, it is a solution. I can write an action for GitHub action to update it.

I don't know what's your opinion. Just to make sure I understand the issue, if I have some ERC20 and I bridge into Cadence and there's some bridge representation, is the problem that it's just not able to be picked up? No, because the template is a flow icon. The display in the template is a flow icon.

There's no on-chain data for their logo. We can't be guaranteed that there's a contract URI with their metadata. I saw yesterday when I was looking at some of the metadata for ERC20 tokens in Metamask.

I think there's a way that you can add it, but it's off-chain. The idea of using something like some GitHub repo to pick up that metadata is a good idea. We can use it this way, maintain an asset repo to include every logo, JSON file, logo, image with an EVM address.

We can read from the off-chain way. I guess that makes sense. It sounds like that's probably a path forward for that. 

We just want to make sure that that's documented so that anyone who deploys in ERC20 or in ERC721 knows how to make sure their logos are picked up and well-rendered properly. Another question is about is there anyone who wants to maintain the list? For example, previously I maintained a vulnerable token list for add features, add verified tag for this token. Also, currently I added a blocked tag for some token that did not display good enough for some marketplace. 

They can choose query the token list with a reviewer address then they will get reviewed information from this reviewer. Is there anyone who wants to maintain that list or just let me do it? I don't know because we need to always keep an eye on the list and check the information and it takes some time to do it. That sounds like an operational, organizational figure out how.

It's open source, right? Yes, open source. Anyone who wants to do it will do it since it's just a problem. What would that process look like? Someone has to submit something to some GitHub repo? No need to GitHub repo, just all in these websites.

There are the maintained token lists. Yeah, it would be probably helpful to have some sort of event indexing and notification and Discord so that the community can at least know that there was something that was submitted in a central place that's highly visible and then someone can go into that website and take action as a reviewer. Kind of like what you would set up for a PR Slack bot or something like that or an issue Slack bot but we're not working with GitHub or Slack so it'd be kind of like a more community oriented version of that using the contract and Discord.

There are no other questions for me. I do have one other question. I'm trying to sort out what steps someone would need to do after deploying a token via NFT or EVM or NFT or fundable token on either VM to make sure that their assets are picked up by token list and that the metadata is displayed how they want to. 

Considering also that they may only deploy to one side and then onboarding may occur later. My question is for the actual path of I deploy some contract and cadence and then I onboard a token list but I'm not onboarded to the bridge yet. If at some point later it's onboarded to the bridge.

Yeah, token list already I just use a token list onboarding to the VM bridge. It's just one click operation like here. Just like input the address here pick the token and then onboard to the VM bridge.

You can just update settings. So it's just one click. You can register the token list then onboarding to the VM bridge.

One click. Oh, nice. Okay, that's really cool. 

And so if someone's already onboarded onto token, like if they're already registered in token list then that will just onboard them to the bridge. Yeah, that's very easy to use. But it's manual, not automatically.

Because you will see the transaction I'm using here transaction register standard assets or register EVM assets register EVM assets will be directly onboarding to VM bridge and register to the token list. And register standard assets like vulnerable token, non-vulnerable token, you can choose not to onboard to VM bridge. And this is a single line to register in the token list. 

But if you want to onboard to the VM bridge, there will be another more complex transaction. So a little bit of difference. But yeah, so it's just transaction I'm using in the website.

Okay, yeah, that makes sense. Yeah, I guess on the topic of the VM bridge and as it relates especially to NFTs. So currently in metadata views, there's not a way to define an NFT symbol.

Just like for fungible tokens, their fungible token metadata views, the FT display I believe is where you can define your token symbol, but there's nothing comparable for an NFT. At least there wasn't. Now there's the EVM bridge metadata, which either a contract or a resource, an NFT or vault can define and the bridge will use that information to set EVM metadata. 

And in particular for NFTs, that allows you to define a symbol. But totally understanding that most NFT projects probably hadn't implemented that metadata view. So in the bridge there's the ability, or at least on the EVM side there's the ability to update the NFT symbol. 

So I have to add in the ability into the bridge to pick up any updates to an NFT symbol, but that's something that might be also helpful to add into token list once that functionality exists on the cadence side to basically say sync metadata for this NFT collection and it would update the symbol on the EVM side. Is there an extra view we need to include in this token or just like a method I can call on the token list, just like update because the view from token list is a contract inside token list to just save a separate view reserver. If you edit a display, it's just like only used by token list. 

Oh, I see. So there's a specific view for token list. It's not a specific view, it's a specific view reserver. 

It's another resource for view reserver to maintain the editor. You can see here is the editor. If you edit the view, you can update a lot of information as a reviewer, but if you didn't modify anything, the view reserver is from the resource contract. 

If you see this token, all the metadata load from the contract, but if you add anything here, you will create another resource, implement view reserver, and the new view reserver resource is a new resource inside token list. So it is a little bit different from the original one, but when you get the list, just merge the data first from the token itself, and then if you pick a reviewer, the extra data will be using the view reserver data from the reviewer first, then if you're missing some data, then you get from the original one. So I guess what I just pasted is the metadata view that's included in the standard metadata views, and so that would allow a cadence native project to define their own EVM metadata, and so a contract that hasn't implemented that or an NFT that hasn't implemented that can, and even after that asset has been onboarded to the bridge, which would have programmatically derived some symbol from the NFT contract name, once this metadata is set inside of the base contract, that metadata on the EVM side can then be updated to whatever the contract says it should be.

And so that's implemented to allow for cadence native projects to define a bit of their EVM metadata, even though they can't necessarily control the corresponding ERC721. So that's kind of what I was referencing too. So if a contract hadn't included that metadata view and defined their symbol before the asset was onboarded to the bridge, they can define that in their cadence contract, update their contract, bridge, and then basically sync the EVM metadata after they've defined it for themselves. 

And so that's just kind of the base layer. I think that can exist in conjunction with the reviewer system and the token list specific views set by reviewers. But I think it's still important to have that just so that if someone wasn't even aware the token list existed, they would still be able to get information about the NFT as the project itself defines it.

Does that make sense? I'm taking a step back. So I'm wondering, I really like Gio's idea of the Slack bot notifications, and I'm wondering if the simplest solution might just be creating a React webhook that integrates with Slack essentially every time someone submits or edits or verifies, then a notification gets sent directly from the front end to Slack. I've done something similar before and it wasn't too crazy because then we wouldn't have to depend on anything happening on-chain.

It's whenever people are just on the application doing stuff. Would that be a potential route? Is that a spam vector? Spam vector, yeah. I mean, I guess people could just spam, like create a thousand NFTs and just add them all to token list and then it would technically spam that Slack channel.

Gio? We already have a Discord bot for contract deployments and updates on both testnet and mainnet. I don't know that the vector is any different than that. I guess that's what I was thinking, something more so that's more highly visible within Discord because Slack is primarily internal.

It probably would be very similar to whatever the infrastructure is that supports that. You're just listening to a set of events and posting a message whenever one of those events fires with some of the content of that event. Whoever set that up, I'm imagining it's probably the fine team or VRT specifically would be familiar with how to set that up.

Ohao, would you be down to maybe sync with VRT and investigate what the possible avenues could be to notify when those changes get made so that we minimize the chances of not maintaining it? Sorry, you mean like keep track through metadata view of NFT who may be missing a bridge metadata view? So we need a FlowDiver or a FlowScan to keep track of that and have some notification? Something like that. It's more related to the point that you made earlier about the challenges of maintenance, like who's going to maintain everything. This could be a semi-automated way to identify potential risky changes as they pop up.

I don't know. VRT has just answered this question about who wants to maintain more centralized like someone from 14 to maintain something like that. But yeah, it's a question about maintenance or about having a notification about updates.

I guess maybe Sorry, I didn't mean to interrupt. Maybe the suggestion for that is based on the idea that someone submitting their project to TokenList needs to be reviewed and that that review should be done by someone. That's how I interpreted the meaning of you saying we needed to maintain it. 

Someone needs to know that new projects are submitted and then someone needs to go and review them. Or do you mean like Why I built TokenList is I don't want anyone to block the process. It's just a permission list that anyone can use.

Now TokenList is like this one. But if we include any review process on board, there may be a lot of scams there. I don't know. 

I just don't know. Just to help us understand, I'm not sure if we're all clear on what needs to happen to maintain. When you say maintenance, what type of maintenance Just like keep an eye on the scam or keep an eye on the broken NFT and help the broken NFT or vulnerable token not in the list and feature some, for example, USDCF that has a feature.

I can maintain for the vulnerable token, but I'm not really good on how to maintain a non-vulnerable token process. It looks like more non-vulnerable token than vulnerable token. Vulnerable token is easy to maintain.

Do you mean adding new non-functionable tokens directly to TokenList in a more automated way? Would that solve it? It is an automatic way. But for TokenList and NFT.js, I'm only concerned about checking the collection data. I didn't have a double check on NFT. 

I didn't have a deep check if the URL is broken or if the icon is broken. If the URL didn't get anything, I didn't check this one. What I mean by maintain is that it's also like BRTech asked, is there anyone to check everything? Yes, there is a view there, and it's valid because there is a view there. 

But you still need someone or maybe some boot to check the list and give the token a score. Okay, the URL is valid and everything is valid. Something like that.

Okay, so it sounds like that's something that we may be able to set up programmatic checks on. Yeah, but it can be next step. Just for everything to work.

In the meantime, basically that would be done when for example, someone submits their project to TokenList. I have my project and then TokenList picks up the metadata views and the URL and the image and all that stuff. That's when I would imagine that at least at first taking place this cursory, not review from the place of being a gatekeeper, but reviewing just to make sure that everything is good to go and looks solid.

That's maybe where something like a Discord alert would be helpful to know that there are... Yeah. I will show something that's really cool. Howl told me he is working on build the TrustWater core like a general water library for a lot of water. 

He's using TrustWater core and TrustAssets for integration like a blockchain, EVM compatible blockchain.

(This file is longer than 30 minutes. Go Unlimited at TurboScribe.ai to transcribe files up to 10 hours long.)
