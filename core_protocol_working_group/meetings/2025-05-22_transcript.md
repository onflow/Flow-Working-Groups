# Meeting 13 - Core Protocol Working Group
**Date**: May 22, 2025 (Thursday), 10-11am PT (17-18:00 UTC)


**Meeting Room**:
We have a protocol working group, no agenda, nothing to talk about.

**Meeting Room**:
That's fine. I thought there was one you and Dennis had a discussion about this, where he had a topic. Yeah, yeah, I saw we did that already on the last call protocol workflow. I misunderstood as this one. Oh, maybe I misunderstood it.

**Meeting Room**:
Do you remember where it was?

**Meeting Room**:
Do we have any leftover things from previous?

**Meeting Room**:
No. I don't think we have. I mean, Tarek has already talked about his stuff, right? There was something he wanted to tell, but that was why I was out. You did that. Yeah, we did that. And that was done.

**Meeting Room**:
All right. Yeah.

**Meeting Room**:
Hey, Peter, I think I screwed that up. We have a core protocol working group meeting, but no topics on the agenda. Nothing to talk about, I think. At least nothing I'm aware about.

**Peter Argue**:
Yeah, I don't have anything to talk about now either.

**Meeting Room**:
Pete, do you have something you want to talk about?

**Dieter Shirley**:
I always want to talk about stuff, but I can't think of anything off the top of my head. We don't have any externals today? That's disappointing.

**Meeting Room**:
No, I don't think we have any externals.

**Dieter Shirley**:
Maybe we can talk about the good stuff for a change, huh? Am I right?

**Meeting Room**:
Stop wasting my time, Deet.

**Meeting Room**:
I don't know.

**Dieter Shirley**:
No, I don't have anything.

**Dieter Shirley**:
But I think I'm glad we all joined, just in case an external did join. But the only thing, hey, oh, actually, this is just a question for you, Alex, while I'm thinking about it. What is Faye working on on the Tri research?

**Meeting Room**:
I assume she's doing Speaking of that storage serialization topic, we talked about the last time. Do you remember? Oh, there is somebody. Okay. Someone is from outside.

**Dieter Shirley**:
What do we tell them? Let them in. We'll just let them know that there's no bugs now.

**Meeting Room**:
All right.

**Meeting Room**:
Who is it?

**Meeting Room**:
Joshua Ayo Hey. No one joined.

**Dieter Shirley**:
I guess he left. We took too long to let him in.

**Meeting Room**:
Or maybe you clicked on the wrong button.

**Meeting Room**:
So the storage upstream, remember we talked about if you had individual snapshots of the drive, how you would write them into a storage container? Yeah. And then sort of how to chain them, one version to the other. Yeah, I think that's currently what Faye is working on. Hey Joshua, welcome.

**Unidentified Speaker**:
Any ideas?

**Unidentified Speaker**:
Hello.

**Unidentified Speaker**:
Hi.

**Dieter Shirley**:
We don't want to put you on the spot, but we don't have any topics for today and since you're the only non-foundation person to join, now I kind of want to find out what you work on and your interest in flow is. I think Joshua was not expecting to be the star of the show. That's no problem, my friend. Thank you for joining us, nonetheless. But as I was saying, the protocol team doesn't have anything, any topics to discuss today. So unless you have some business to raise, then we'll probably adjourn here.

**Dieter Shirley**:
Thank you so much for joining us, Joshua.

**Joshua Ayo**:
I'm sorry, we can't we can't hear you.

**Dieter Shirley**:
I don't know if it's a problem with your microphone signal.

**Joshua Ayo**:
I just switched from my router to another signal set, which is a bit faster than a router.

**Dieter Shirley**:
Yeah, we can hear you just great now. Yeah, did you want to introduce yourself and tell us what you're working on?

**Joshua Ayo**:
Let's put it that way. I'm a blockchain developer. I mostly work with EVM chains. I currently work with EVM chains. I work with Flow once or twice, but the calendar is still in my calendar at least. So I'm going to see if there's any improvements in what is happening in Flow community to see if there's anything new I can actually go and try out for learning sake. I'm not building any project right now.

**Dieter Shirley**:
Oh yeah, and I'm based in Nigeria. You do know that Flow has full EVM support now, do you? Yes.

**Joshua Ayo**:
I think I saw the message. I go to Gmail. I never did DeepR. So, is which programming language Solidity? That's right.


**Joshua Ayo**:
Or is it Cadence?

**Joshua Ayo**:
It's both now.

**Dieter Shirley**:
So, we kept the Cadence environment, and what we were able to do is embed EVM with Solidity inside Cadence. And so, if you're an EVM developer, you can just interact with Flow the way you interact with any other EVM chain. But if you're a Cadence developer, you get all of the features of cadence and you can call into the EVM. And so you can build hybrid applications. So you could take, for example, Aave, you could take a fork of Aave, deploy it in the EVM environment on flow, and then add additional functionality using cadence that calls into the EVM. So any of the parts of Aave that you want to reuse, you just reuse the solidity code, anything that you want to do in Cadence that isn't possible in Solidity, and a variety of features, especially around composability there, then you'd be able to write those in Cadence. And so it sort of gives you the best of both worlds. So if you have any existing projects in EVM that you think could be advantageous to the Flow ecosystem, now is a really great time to bring them over.

**Joshua Ayo**:
Okay. Okay. That's nice. I would look at the docs a little bit more and YouTube videos if I find any.

**Meeting Room**:
For sure.

**Meeting Room**:
Yeah. Emerald Academy https://academy.ecdao.org/en

**Meeting Room**:
Did that go? Yes. They're really good source for tutorials and videos. I can highly recommend And then the other great resource, of course, is if you want to join our discord, you know, there you can ask questions.

**Joshua Ayo**:
You're already there. Nice. Thank you. I joined during the period.

**Joshua Ayo**:
All right.

**Dieter Shirley**:
Yeah, I think it was like a year ago or so.

**Meeting Room**:
Very cool.

**Dieter Shirley**:
Well, thank you so much for joining us, Joshua.

**Meeting Room**:
I hope you have a great rest of your day, and hopefully we'll see you again. Yeah, please come by if you have any protocol related questions.

**Joshua Ayo**:
And yeah. If you have now, go ahead. I do have a little, it's like the way you, is this from what Shirley, I think, said earlier. Was um yeah I'm trying to see here um how you put in if you're a cadence developer you can wrap evm and still write the cadence so is it like the right solidity in cadence and still reduce the cadence or like right solidity on top of cadence that level like if you don't mind going to like nitty-gritty a little bit because I'm very curious about things like that when it comes to like cross-bordering of like blockchains because it's really an topic and it's not always well done. There's always this ish there that you really need to like look into. And, you know, enormous gas fees, one of the two. Yeah.

**Dieter Shirley**:
So I'm happy to talk to you about this for a little bit. The rest of the team actually doesn't, they don't, they don't work on cadence and EDM. So maybe while, if your, if your questions are about cadence EDM, then maybe we can let some of the folks go, but I'll stay on for another five minutes and I can give you the basics. How does that sound?

**Joshua Ayo**:
Yes, okay, thank you very much for your time. Yes, I'll definitely go. Okay, cool.

**Dieter Shirley**:
Okay, so if any of you protocol guys want to drop off, you're welcome to, and if you want to stay and hear me pitch Flow EVM, by all means, hang out. So, Joshua, the I think the one analogy that I think is very helpful is to think about if you're writing in a language like Rust, you might want to use a C library. And so you don't copy and paste the C code into a Rust file. You compile them separately, but one is able to call the other. And that's how we did EVM. So the way it works is if you want to have a hybrid application, you deploy your EVM, your Solidity smart contract into the EVM environment. And then your cadence code has the ability to create these sort of synthetic or mock addresses that live inside the EVM and can do anything that like a normal smart contract or EOA in Solidity can do. But it's cadence that decides what they do. So in cadence, you have this data type called owned account, or as we call it a COA. And that thing you can, it's basically an Ethereum account, or you know, an EVM account. And it can call smart contracts, it can own tokens, it can transfer tokens. And so anything that you could, you can almost think of it as like, if you were to write a script on your local machine, maybe using Python or Node or something like that.

**Joshua Ayo**:
Go ahead.

**Joshua Ayo**:
I was like, that sounds like something a contract address would do, where you keep like the file, like the logic inside. So the contract address is able to be called on from the EVM in cadence. So you create like communication via contract address, something like that. It's like when you're doing like upgradeable contracts, where you route from the past contracts to improve on it and on that contract, but you're still calling the base functions from the previous contract.

**Dieter Shirley**:
Yes, exactly. That's a great analogy, right? So you can sometimes do this in Solidity, right? Where you're calling, you know, you have a new smart contract that's calling an old smart contract. That's exactly right. And except that you're doing it from Cadence. And because Cadence is a more expressive language, you can do some pretty interesting things inside Cadence that you wouldn't think to do inside the EVM. So for example, in Cadence, because the EDM addresses are individual cadence objects, you can have a smart contract or an object on the cadence side that controls three or four different accounts on the EDM side. You can create temporary accounts just for the course of a transaction. So for example, I wrote a sample application. I was just playing with it, but I wanted to demonstrate that you could use the DEXs that were deployed on EBM from the Cadence side. And so what I would do is I would take an account that has some tokens on the Cadence side. I would create a temporary Ethereum account. I would bridge those tokens between the VMs. So I'd take the tokens from Cadence, put them into the EBM, then call the swap function on the AMM. It was Kitty Punch was the AMM I was using, which is I believe it's a Uniswap fork. And I would do the swap and then I get a different token, a different ERC20, and then I would bridge that back. And so within the course of a single transaction, I was bridging tokens in, swapping them on the EVM side. In some cases, I would swap them twice, right? Trying to pick up arbitrage opportunities where doing a swap between a token would give me a better price than swapping directly from one token. Into the other. And so I could do two swaps. And from the standpoint of Kitty Punch, it looked like it was just two people, two different transactions. But from the standpoint of Cadence, it was all one transaction. And so the whole thing is revertible. The whole thing is atomic. So I didn't have to worry about any front running or back running or injection attacks into that stream. I could do as many things with the EVM as I wanted inside that one Cadence transaction. And everything was all atomic. And so it allows for some pretty powerful functionality. We're talking to some developers now who launched OnFlow after we provided EVM support. And their first release was 100% EVM. You had to use MetaMask in order to interact with their product. Their whole front end was built using RainbowKit and all of the EVM infrastructure. And now they're starting to look at how they can use cadence to improve add improve features. So, you know, very simple things like instead of just using multi call to do multiple data queries, they're able to use relatively complex cadence scripts in order to query multiple parts of the EPM state and maybe even do some processing and formatting of that data on in the script rather than having to do it on their servers. And so there's there's some pretty interesting efficiencies to be gained. And what we're seeing is that I think anybody who's programmed Solidity for very long, they feel the edges of that programming language. It's pretty restrictive in some important ways. It's also obviously very powerful in some important ways. And Cadence, now that we've got EBM and Cadence together on the same chain, able to talk to each other synchronously, atomically, then you really can get the best of both worlds where you're taking all of this existing DeFi logic and understanding and you're able to wrap it in this language that is capable of doing more advanced things.

**Joshua Ayo**:
Okay, moving on. So sorry, I just had one more question. I want to ask about wallet abstraction in Flow. We know the old wallet abstraction analogy So when you don't need a wallet, because I see they have to use MetaMask. Currently, anybody that's currently building on blockchains are trying to like abstract wallets. And this is a very key major functionality. That's something I always want to work with whenever it comes to documentation and like working with. So do you currently have wallet abstraction on probabilities of flow? Or is it something you think about if I can create an EVM compatible version Let me first ask if it exists correctly before I go on further with what I'm thinking about.

**Dieter Shirley**:
So yeah, the account model and the way that wallets work is something that we really wanted to expand what's possible in Flow. And so our account model and a cadence account is not tied to a key. A cadence account is an independent entity that can have keys and it can have code. It can have both. I mean, theoretically it can have neither, but that's not very interesting. And in particular, it can have multiple keys associated with it or multiple pieces of code associated with it. And so we're used to thinking in EVM of, you know, just, you know, there's an account, like there's an address and it's either code or it's an EOA. Now with Petra, we have the ability to add code to an EOA. But in Flow and Cadence, it's always been the case that you can add as much code as you want to any given one account. You can add as many keys as you want to any one account. And critically, you can remove those things as well. And so, you know, if you have an Ethereum account address that you think you might have lost the key, you have to move all of your assets out of that to a new address. And if any of your friends have that address or whatever, then, you know, it's a big pain. On Flow, you just remove that key and put in a new key. In addition to that, we've created some pretty powerful mechanisms that allow one account to have control over another account and put limits on that control. For example, as an application developer, I can say, look, when users come and first start using my application, they don't want to think about keys, they don't want to think about a wallet, so I'm going to manage their key. I'm going to have a key, on their account. And when they come, they'll just log in with username and password. I'll manage their account on their behalf. And so long as they're doing really simple stuff, if it's a game, they're not, there's no money involved, I'm not worried about, you know, financial regulations and things like that. They're just, you know, maybe collecting NFTs in my game, I can just use a normal web to style password flow. And I can manage their assets on the chain for them. It's no no worries. Now, obviously, that's centralized, right? And And other people will come in and say, no, I do want to control my own key. Maybe even that same user that came in and when they first started using their application didn't understand the power of blockchain. Now they do. And so because we can take that same account object and you can remove your key at the same time as you add their key, you can hand that account off to them without them having to transfer any assets or anything like that. They don't have to change their identity. And the assets, they just, now they have the key instead of you having the key. But even more powerful is you give them account, you put a key on it, and then you also maintain a limited capability on their account to do certain things. Maybe it's, oh, well, here's your account. It has all of your assets in it. You can go and play with DeFi with this account now if you want, but I still want to be able to, for my game, I still want to be able to move your NFTs around. But I don't want to touch your finance, right? And so you create a limited capability on their account that lets you manage their NFTs, but not touch their financial assets. And all of that is possible inside Cadence. And so it allows the very powerful mechanism, we call it account linking. And it can be done with when you create a new account, it can be done with existing accounts. And it's something that NBA Top Shot is using. So if you've ever looked at NBA Top Shot, previously, when it first launched, all of the NFTs were inside that one application, that one central login. But now you can connect a wallet to your TopShot account, and you can go and trade your NFTs on OpenSea, for example. And so they've used that account linking functionality to make it so that if a new user comes in, their experience doesn't change. They just log in with username and password. But if a Web3 native comes in, they attach their wallet and their NFTs are controlled by their own key and whatnot.

**Joshua Ayo**:
Wow, that's a lot. That's nice.

**Joshua Ayo**:
Oh, thank you.

**Joshua Ayo**:
Thank you for that. I'll dig into that a little bit. I see you sent me a link.

**Dieter Shirley**:
Alex posted a link to that functionality. Exactly.

**Joshua Ayo**:
Thank you very much.

**Joshua Ayo**:
So yeah, we'll look into because I've been digging into account abstraction of recent like on variety blockchains because like there's a two version for zk-sync and the ethereum version of it so yeah been digging into how to like put it into other chains and will be um interested in furthering it so with this account linking I'll just go through the docs and see thank you very much on this because I have like some Well, thanks so much again for coming out, Joshua.

**Dieter Shirley**:
And thanks to everyone else. Have a great day, folks.

**Joshua Ayo**:
Have a great day.

**Meeting Room**:
Bye.