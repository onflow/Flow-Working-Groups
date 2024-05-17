# Joint Meeting of the Cadence-Execution and Core-Protocol Working Groups on May 15, 2024 - Transcript

**Attendees**

Alex Hentschel,
Andrii Slisarchuk,
Austin Kline,
Bastian Mueller,
Deniz Mert Edincik,
Dieter Shirley,
Faye Amacker,
Felipe Ribeiro,
Giovanni Sanchez,
Greg Santos,
Gregor Gololicic,
Illia Malachyn,
Jan Bernatik,
Janez Podhostnik,
Jerome Pimmel,
Jordan Schalm,
Josh Hannan,
Khalil Claybon,
Layne Lafrance,
Navid TehraniFar,
Ramtin Seraj,
Supun Setunga,
Tarak Ben Youssef,
Tom Haile,
Uliana Andrukhiv,
Vishal Changrani

## Transcript
*This editable transcript was computer generated and might contain errors*

**Alex Hentschel**: Welcome everyone. So this is a joint meeting of the Cadence and execution working group and the core protocol working group. Our main topic today is EVM compatibility.

**Alex Hentschel**: 
Deet has volunteered to be our master of ceremony today. Thank you, Deet. I'm going to hand that over to you in a minute. You said you had some slides. I'm not sure. I don't have super much experience with managing who can present and how that works. So I hope it's going to be smooth, but if not, my apologies up front. And yeah, with that, Dieth, do you want to present slides?

**Dieter Shirley**: 
Thank you.

**Alex Hentschel**: 
Hey, it's working. Love this. Oh, and we need to record, right? Oh, yeah. Oh, I can't record. No way.

**Dieter Shirley**: 
I'm not allowed to, even though I created this meeting. Sorry. How do you do that? I can't see it either.

**Alex Hentschel**: 
So if you do want to take on the three dots at the bottom next to the hangout button, it says at the top recording unavailable for me.

**Dieter Shirley**: 
Yeah, same here.

**Alex Hentschel**: 
Who created this event?

**Dieter Shirley**: 
I did. No, Vishal did. Can you, are you able to turn it on Vishal?

**Dieter Shirley**: 
Yes. Oh, Tom can. Yeah, I can. I think that's why, because I'm not logged in as my dapper. I'm logged in as my flow foundation.

**Alex Hentschel**: 
And can you add the transcribing function too from Google, Vishal, please?

**Vishal Changrani**: 
I'm not recording, but yeah.

**Tom Haile**: 
Well, let me see. Let me stop and then restart it because there's a checkbox. There's got the checkbox. All right, button clicking.

**Dieter Shirley**: 
That's really all we do is click buttons and let the computers handle the rest. All right. Transcription is on. I am ready to present. So I'll try not to take too much time and hopefully that most of the folks here, this will be a bit of a repeat and there won't be anything alarming or surprising. I just wanted to, before we hand it off to Ramtin to talk about some of the details, I just wanted to talk about what our sort of intentions were and our thought processes were in coming to EVM on Flow and sort of how it, why it may look the way it looks and what our thinking was in shaping it the way we shaped it.

**Dieter Shirley**: 
So, you know, EVM support is something that we've heard from a lot of people when we go to, you know, sort of Web3 conferences generally, talk to the Web3 ecosystem generally. A lot of people are very interested in Flow and what we're doing over here. But, you know, they have an investment in EVM infrastructure. And so it's something that we looked at, we wanted to have support for for a really long time.

**Dieter Shirley**: 
But there was some sort of design goals that we weren't willing to give up. And the first one was this notion of EVM equivalence. So that term first came from the optimism team. And the idea was is that it can't just kind of sort of run solidity code, because people have an investment in code and infrastructure. And a lot of that code has been audited, it's been battle tested, that infrastructure has existed for a while.

**Dieter Shirley**: 
That unless it works exactly the same way that Ethereum works, up to and including the APIs you're talking to, exactly how the opcodes work, how much gas is being spent on things, Then there's a risk that you can't deploy on that platform because some subtle behavior will be different and the things that made your thing secure or correct will no longer be true. The example from Optimism was that they replaced their...

**Dieter Shirley**: 
transparently bridged the native token to an ERC20 so that when you did an ERC20 transfer of their native token, it would update your native balance. I'll stop talking because unless you know the details of EVM, this isn't going to make any sense. But the point is, is that they tried to do something clever to make things easier, and it broke an assumption of some smart contracts. And by breaking that assumption, those smart contracts were no longer secure.

**Dieter Shirley**: 
And so So we knew that it kind of sort of runs EVM or it cross compiles EVM. That wasn't going to solve the problem that people actually wanted solved, which is I can adopt this platform without having to rethink my code or my security model. The second thing that we were unwilling to give up on was composability with Cadence. There was no way, for me specifically, but I think the team in general, we're going to have a world where the Cadence world and the EBM world weren't friends, that they didn't talk to each other, that they didn't interact with each other.

**Dieter Shirley**: 
Because that kind of defeats the whole vision of Flow, which is about composability. It defeats the whole value of having additional applications and assets being deployed on Flow if they don't work nicely with the other applications and assets that are already deployed on Flow. And the last thing we wanted was to put a bunch of effort into EVM and then have EVM not be cross-compatible with Cadence and have the EVM maybe just end up being a checkbox feature rather than something actually useful to people.

**Dieter Shirley**: 
Or the EVM, you know, getting a bunch of utility and then the Cadence applications feeling like they're sort of left out of this thing. So neither side could be an island. There had to be connected. And the final thing was is that we wanted to make sure that even if you came to Flow with an EVM project and you had all this EVM infrastructure, that you could get access to the features of Flow that,

**Dieter Shirley**: 
some of the features of Flow that we're most proud of Obviously, cadence is a big one, but our account model and how we manage ownership and how we manage access and the ability to do key cycling and use Secure Enclave, all that sort of stuff. A lot of the value of Flow comes from those features that if it weren't open to EVM projects, there's kind of very little value in coming and running your EVM project on Flow if you can't get access to those features.

**Dieter Shirley**: 
But many of those features are because we fundamentally broke assumptions that the EVM made, right? For example, one of the assumptions in EVM is that your account address is your public key. And we broke that.

**Dieter Shirley**: 
And I literally said this for a long time, because people would ask me, let's do EVM on flow. And I would say, look, these are the things that we can't give up on. And it's impossible to do EVM on flow without this. And it's thanks to Ramtin and a bunch of brainstorming and work we did together. But I have to give credit to him, that we came up with this idea of baking the EVM as a virtual machine, sort of Docker-like, into Cadence that we realized that we could sort of have our cake and eat it too.

**Dieter Shirley**: 
And so the conceptual design is that the EVM is inside Cadence. You can think of it as a smart contract. There's a smart contract inside Cadence that emulates the entire EVM. And when you're an EVM client, you actually, you know, we put these machines up called gateways that talk this sort of normal JSON RPC that Ethereum nodes talk. And they transparently wrap that code in, you know, the transactions provided in cadence or the state queries in cadence scripts.

**Dieter Shirley**: 
But then they can see into the EVM environment. This limitation that EVM clients can only see the EVM environment is, I don't think there's any way to break that down. The nature of cadence and the cadence environment is more expressive, more complex, has more dimensions than EVM does. And trying to represent cadence inside EVM is, more or less impossible. I kind of think of it as like, I don't know if anyone's ever read the amazing short story Flatland, but you know it's this idea of what would it be like to live in a two-dimensional world and a three-dimensional guy goes and starts talking to a being that lives in a two-dimensional world and I kind of feel like EVM has one less dimension than cadence.

**Dieter Shirley**: 
And so we can map EVM into the cadence environment, but we can't map cadence into the EVM environment. Cadence, on the other hand, sees everything, right? Cadence can see EVM, it can talk to EVM, it can understand all of the internals of EVM. And so if you're in cadence, you get all of EVM, but you also get all of cadence. The other important thing that we did was to support cross-VM token transfers.

**Dieter Shirley**: 
So, you know, more complex objects in Cadence can't be represented in EVM. More complex smart contracts inside the EVM, they can be talked to from Cadence, but you can't really represent them as Cadence data types. But ERC-20 and ERC-721, the fungible, non-fungible token standards on Ethereum map can map more or less to the fungible token standards and non fungible token standard on inside cadence.

**Dieter Shirley**: 
And so what we've done is actually build a mechanism so that you can transfer tokens from one side to the other. And so assets that are defined can more or less be bridged to the other side. And so If you deploy an EVM token, it works in all of the Cadence smart contracts without those smart contracts making any changes at all. If you deploy an NFT on the Cadence side, that NFT can be bridged into an ERC721 smart contract on the Ethereum side and EVM only code can understand that.

**Dieter Shirley**: 
So that's a really critical aspect of that composability. Then Cadence accounts actually own EDM accounts, and it's actually a one-to-many. So it's not a mapping, it's an ownership. And so your Cadence account can own multiple Ethereum addresses. It won't always be the case you'll do that, but if you're a developer, it can be very handy to potentially have multiple EDM addresses. And then the other mental idea that I want folks to keep in their mind is that one way, especially as a developer, that you can think about the way Cadence and EVM talk to each other is that Cadence is to EVM almost the same as Rust is to C.

**Dieter Shirley**: 
So if I have a bunch of, if there's a library that does what I need, I'm a Rust developer, there's a library that does what I need, it's written in C, I don't have to rewrite that library to use it in my Rust application. I can just take that code, at ccold wholesale and put it inside my Rust application.

**Dieter Shirley**: 
The reason I use C and not some other language like, say, Go or Python is because, like the example of Rust and C, the example of Cadence and EVM, there's very little in the way of efficiency improvement, right? Like, there's no, you know, if you wrote Python code, you might want to intentionally write C code for performance reasons from your Python. That's not the case, and I hope no one thinks that way about writing code in EVM.

**Dieter Shirley**: 
We're working very hard to make sure Cadence is highly efficient. There may be situations today where EVM is a little bit more efficient than Cadence, but we're going to be putting a lot, a lot, a lot of effort into improving the efficiency of Cadence. And I don't think that same effort is going to go into the EVM side, because we're drafting off of the EVM implementation from the Ethereum community.

**Dieter Shirley**: 
This is not a net new EVM implementation. We are using the code directly from Geth. So I would expect to see that cadence logic will get faster over time, whereas EVM logic will probably not speed up. So I would encourage you to use cadence for net new code. But if you have existing code or you know existing code in EVM that you want to leverage, by all means, make use of that.

**Dieter Shirley**: 
I think it's useful to think through three different personas in terms of how they're going to interact with EVM on Flow and how they might think about it differently. So the first persona are cross-chain infrastructure providers, you know, projects who are inherently interacting with multiple blockchains and it's fundamental in their functionality. The next group we'll talk about is the people who are building EVM based applications that have some sort of, you know, direct consumer facing.

**Dieter Shirley**: 
I don't just mean consumer facing as in like, you know, like, you know, it's a game or something like that, like you'd be defiring like that, but where end users are using it directly. Often these infrastructure providers, they're providing functionality to developers. This is where you're providing functionality to end users. And then of course, cadence app developers is, is a very important group and I want to talk about how they should think about EVM as well.

**Dieter Shirley**: 
So cross-chain infrastructure, for the most part, they don't even need to think about the cadence side of things. They can just talk to flow as though it's an EVM chain. And and depend on the fact that all of the token bridge, the ability for Cadence to see inside the EVM and to call code inside the EVM, whatever infrastructure value they provide to the chain will be, by making it available to EVM, they are making it available to Cadence without any extra work on their part.

**Dieter Shirley**: 
And I give some example here, like price oracles feeding data into the EVM, you'll be able to see that from Cadence. Bridges, bridging tokens from other things can be bridged back into cadence. Centralized exchanges, you know, the ability to do deposits and withdrawals directly on chain, if they choose to go EVM only for that integration, because that makes their lives easier. Well, that's fine, because if you have a flow reference wallet, or some are FCL wallet, you can still interact with those, with those centralized exchanges.

**Dieter Shirley**: 
And cross-chain DEXs as well, you can sort of think of them as cross-chain infrastructure. They're kind of a mix because they also tend to have a direct user facing. But if you are working cross-chain, you probably already have to dip your toe in MetaMask. And so the fact that these kinds of applications may only work with MetaMask is probably fine. And so in terms of Cross-chain infrastructure, it's kind of the best of both worlds where the cross-chain infrastructure team who typically already have the ability to support EVM chains can just add flow to their list of supported chains, but all the cadence developers get all the benefits of having a chain, we're building on a chain that has that infrastructure available to it.

**Dieter Shirley**: 
On EVM apps, if you're an EVM dApp developer and you want to deploy on Flow, if you're okay restricting your users to MetaMask, you're good. You just deploy on Flow and it just works. Cadence NFTs, Cadence Fungible Tokens can be breached into that EVM environment and your EVM only application can work with all of those assets even though it only works with MetaMask. But where I get really excited is EVM dApps at some point in time in the future, and this could literally be the day after, it could be months later, but they can as needed, as desired, starts to add flow specific features without having to rewrite and disrupt their existing functionality.

**Dieter Shirley**: 
So a lot of flow features like account abstraction, secure enclave, account linking, transaction batching, those can be accessed through cadence. By only changing their off-chain user interface code. So if they have off-chain infrastructure code, like back-end code that's like indexing the chain or something like that, that code never needs to understand KDs. If they have a smart contract where all of their logic lives inside EVM, that can stay.

**Dieter Shirley**: 
They never have to deploy additional smart contract functionality. All of these features that you see here, that can all be done on the front end. And they can be in a situation where they're working with flow reference wallet, they're using flow transactions, they're cadence transactions, they're using cadence scripts. All to create their UI while they haven't deployed a single line of Cadence as a smart contract.

**Dieter Shirley**: 
And that gives them access to all of these features. They're still using the same smart contract code they had before. On the other hand, you want to add new features to their smart contract? They can wrap the existing EVM smart contract in a Cadence smart contract. And that's where that Rust to C analogy comes in. You can have this Cadence smart contract where if it's not new functionality, great, you just call into the EVM and have the EVM do its thing.

**Dieter Shirley**: 
If it's net new functionality and you think it'd be better represented in cadence, then you write it in cadence. And to code outside talking to it, it can talk to that cadence smart contract without even knowing that EVM exists on the inside. And it allows those EVM dApps to become full cadence dApps with all of the advantages of that without ever having to go through a step of rewriting anything.

**Dieter Shirley**: 
Cadence DApps on day one, I think it's the same story, right? If you're okay working with FCL wallets, including the Flow Reference Wallet, which is going to support both FCL and Web3, then you don't have to do anything.

**Dieter Shirley**: 
Any assets that get deployed on the EVM side of things can come over and can be used, whether it's fungible tokens, non-fungible tokens, those could be used inside Cadence DApps. You don't have to do any work at all.

**Dieter Shirley**: 
And because we're putting the work into Flow Reference Wallet to support Web3, people who want to use cadence dApps and any of those EDM dApps that haven't done the extra work to support cadence functionality, if they use Flow Reference Wallet, they get the best of both worlds, and they don't have to give up either side. On the other hand, some Cadence apps might choose to add support for, and I say MetaMask, but what I mean is any sort of, you know, Ethereum style Web3 wallet.

**Dieter Shirley**: 
At first, this might seem impossible, right? It's like, well, you can't ask MetaMask to sign a Cadence transaction. So how can I get MetaMask to talk to my Cadence smart contract? And it turns out that there's a pattern that's really common in the Ethereum world, which is doing approvals and user sign rather than direct transactions. In the flow world, we're often, we say to the user, hey, we wanna do this complicated thing that uses lots of different smart contracts, lots of different assets, but you can do that from one transaction.

**Dieter Shirley**: 
The Ethereum model actually makes that very difficult. And so it's very, very common for you to go to a trading platform, whether it's for fungible or non-fungible tokens and say, I delegate you, smart contract, the ability to move my assets around. And then later when I want to do a trade, I do a user sign, sometimes called off-chain message signing. I do a user sign and I hand, not a signed transaction, but a signed data blob to that smart contract.

**Dieter Shirley**: 
And then it, I trust its logic to, it's this second kind of authorization mechanism to go and move my assets as expected, right? This is the way Uniswap works. This is the way OpenSea works. It is a very common pattern. In some cases, it's the only way to do certain kinds of trades. And in other cases, it's frequently used because it's more efficient, right? You can combine multiple user signed blobs into a single transaction and you can sort of get batch, the efficiencies of batch operations by using these.

**Dieter Shirley**: 
There's no reason why you as a Cadence app developer can't create a COA that is owned by your smart contract that an Ethereum user, a MetaMask user grants approval to that COA, right? So from their perspective, they're just granting an ERC20 or ERC721 approval to that address. And that address is controlled by a smart contract. And then you can do the same kind of logic that OpenSea and Uniswap do where they look at an order and see if it's correctly signed.

**Dieter Shirley**: 
You can do that logic inside KDs. You can also do that logic inside EVM if you want. Again, there's lots of examples of doing that. And so if you want to leverage that EVM code, you can do that. But critically, the point is, is that if you support Web3 in your HTML page, and you use the model of approvals and user sign, which most Ethereum users are highly accustomed to, you do not need to deploy a single line of EDM code in order to work with Metamax.

**Dieter Shirley**: 
Now, you do need to do some EVM indexing. I won't get into the details of that here. Your Cadence transactions will need to understand EVM because they need to call into EVM to do some logic there. But you don't need to deploy new smart contracts. You just need to understand enough about the EBM in order to do this approval and user sign flow. And so you can keep, you know, the vast majority of your code, the vast majority of your effort can be inside Cadence and FCL, but you can still add support from NMS.

**Dieter Shirley**: 
I honestly can't tell you whether or not I think that's a good idea. I don't know whether or not we're going to see a lot of users coming with MetaMask and interacting with Flow and be desperate to use Cadence applications and won't be open to using a Flow reference wallet instead. If you take a look at Solana, everyone's very comfortable using a Solana specific wallet. But if you look at a lot of other you know, EVM compatible chains, they all just use MetaMask.

**Dieter Shirley**: 
And certainly, like, and then there's projects like Near, where they have sort of kind of sort of support for MetaMask. And, but it isn't exactly EVM equivalent. So I don't know exactly where this is going to fall in. I think that's got to be up to you as an app developer. But I just wanted to make sure that you know that there's a path there. And if you choose to adopt that on day one, we would want to help you.

**Dieter Shirley**: 
And if you want to take a wait and see attitude and see how many MetaMask users come in, I also think that that makes a certain amount of sense. And you can always add this functionality in later, just by changing your UI, you don't have to do anything on chain. Okay, so that took longer than I expected. I apologize, Ramtin. I hope you can fit your stuff in. But I just wanted to make sure people sort of understood where we were coming from when we did EVM and to think about how you fit into, how various parties fit into that.

**Dieter Shirley**: 
The one thing, actually, the one thing I wanted to mention, y'all shouldn't be surprised if you see people that currently support Flow and have cross-chain infrastructure, and there's a number of projects that do this, actually switch to the EVM side of things so that their maintenance effort is easier, right? So right now, they're often implementing two code paths, right? They have a code path for all the EVM chains, and then they have a cadence path for supporting flow.

**Dieter Shirley**: 
Some of those teams will choose to keep the cadence side running. Some of those teams will switch to EVM.

**Dieter Shirley**: 
We've told them that we're comfortable with either, that Flow gets the benefit of their support, regardless of which side that they're on. And so please don't see it as alarming if you see somebody switch to EVM, especially with the cross-chain infrastructure. There's literally no reason for them to try and maintain both sides. So I think we'll see a lot of teams Both new teams coming into Flow that haven't been able to rationalize the extra expenditure of having another code base will be joining us, but also see teams sort of moving into EVM because that makes their future maintenance easier.

**Dieter Shirley**: 
So please, over to you, Ramtin, and there will be time for, well, And now that I'm taking it up, there might be some time for Q&A about this later, but I want to make sure Ramton has a chance first. So take it away, Ramtin. Let me share my screen.

**Ramtin Seraj**: 
Let's see, is this working?

**Ramtin Seraj**: 
Click here. Oh, this is nice. Okay. Yeah. Thanks for the introduction and motivation. I can skip definitely a few slides and I would be happy to do that. Uh, so today I'm going to present the state of this flip 225, which is EVM compatibility. Um, and, uh, I'm really excited for that, but before I jump into that, I want to thank. Every one of you, because the state of this flip right now is very different from the original one that we drafted.

**Ramtin Seraj**: 
And the reason for that is because we continuously receive a lot of feedback from the community. We were fortunate to be able to run this on PreviewNet. We had a really a good community and then they supported us to do fast iteration break things experiments as we explore these things because this was not something that was done before. It was very new. It was like a lot of time areas of uncertainty.

**Ramtin Seraj**: 
You didn't know if this is going to work or not. And then Thanks to all of you. Now I will present what you all have achieved with this flip. We can skip the motivation. You should by now be highly motivated after this talk. The main question for this flip, because there was discussion of the AVM compatibility in the forum and all of those things, the main question for this flip was how to integrate As it mentions, there was like, we want to make sure we have a level of composability between two environments.

**Ramtin Seraj**: 
We can have atomic operations across two environments. We didn't want to have like another, like message passing or cross messaging or like bridge between two chains or any approach like that. We want to make sure it's atomic. Calls are supported this. We wanted to minimize the change required for tooling and protocol systems. We didn't want to just like have breaking change from both sides and assume that I have to do a lot of things.

**Ramtin Seraj**: 
And the last one is, it seems obvious, but sometimes you have to mention this. We didn't want to sacrifice any safety or security measures or primitives on each of these. Environments. And that was very challenging. And the reason it's very challenging is because both cadence and AVM are They're mentally different environments.

**Ramtin Seraj**: 
They are different in many, many ways, like programming models, clearly, like you have resources on one side, the other side is different. The account and data models are very different. You have a ledger style of, for example, ownership tracking on one side, the other side, the accounts actually hold on to things. Resource consumption, metering, and storage pricing, completely different on both environments.

**Ramtin Seraj**: 
You have gas metering on the EVM side, on the cadence you have this notion of computation and the way that they meter is very different. Search pricing is very different, you have minimum balance on the cadence side, and it is just like one time fee of gas, which is the amount of byte that you are changing. Security primitives is very fair or access control capabilities. I don't know the details about all of those things.

**Ramtin Seraj**: 
And then also even a higher level ones, these standards, for example, the way that you keep a balance or native token balance on Ethereum or like, sorry, all of the EVM chains like Ethereum and other ones, they have different precisions or they have different standards or like NFTs, they have different standards.

**Ramtin Seraj**: 
It was challenging, like how to integrate this. That was the main question and the main question that this flip tried to answer. So, some of the core decisions, just like some of them, because I also did mention some of the other ones, but the very first decision that was there is just like EVM should use Flow as its own native token. We don't want to mint a new token. We want more utility with the current token and any token that is on the EVM side should be breached from the CAD side.

**Ramtin Seraj**: 
And the second important one is like, as mentioned, cadence was to act as a main point of entry. So we want to reuse the flow transaction format. We didn't want to break that thing or introduce a new transaction type, which means that the cadence has to wrap everything about EVM and provide all of the utilities there. At the same time, if we do use the same format of flow transactions and do this wrapping, we want to have the unified resource consumption, which means gas has to convert into computation and the same settlement environment and all of those things.

**Ramtin Seraj**: 
So it's easier to understand how things are working. And also if we consider this as a main point of entry, then we can have atomic operation across environments because it's like single thing that can basically wrap all the functionalities and be like support atomic operations, which is very helpful for the bridging assets and a lot of other operations that I will tell later. And the last one was like, which we added, like a lot of these things I'm talking, it was added over time by the feedback.

**Ramtin Seraj**: 
We wanted to make sure the cadence logic has full control over outcome of executing like EDM transaction. For example, if any specific error happened, like what are the error codes, like what's the status of this transaction, and then So under like the overarching logic on the cadence side can decide how to behave in case of like running a transaction or something failing because of the sequence number or something's failing because of the other factors.

**Ramtin Seraj**: 
The third part of the core decision was like EVMs deploy as a virtual chain, which we discussed, which is we deploy EVM as a cadence smart contract language that you can import. Like any other smart contracts. Then we realized that we need some privilege underlying access because there are some functionalities on the EVM that you need more access for, or you need a different way of interacting with the hardware.

**Ramtin Seraj**: 
So that's the reason this is a smart contract. It's an EVM smart contract, but it has access to some functionalities that is basically implemented natively, and that can gain a lot of performance and a lot of other factors, but in theory, it should be as if we completely re-implement EVM in Cadence, which we didn't do for performance reasons. So block progress is basically trackable through Cadence events.

**Ramtin Seraj**: 
So every time an EVM block is moving, then you can follow the chain of events, and you have proofs for that, you have inclusion proofs and all of those things. It's always another decision. EVM transaction, basically, as I mentioned, is wrapped inside the flow transaction. So from EVM tooling perspective, they can reuse their legacy or other forms of transactions that are supported by EVM without the need to know anything about flow or introducing new types or anything like that.

**Ramtin Seraj**: 
And then we spend a lot of time thinking about several ways of cross-environment interactions. Obviously, the first one, which is used by some other platforms, was rule out for us, which was shared memory access between two environments. Cadence has like this higher level of like safety measures that we don't want to jeopardize by providing raw memory access or anything like that. So we opt in for like cross calls in a way that we can cover as much as like applications as possible.

**Ramtin Seraj**: 
And during this flip, we came up with three ways of communications between these two environments. The very first one is Cadence calls to EVM. So Cadence can see everything. I mentioned there's EVM smart contracts, so you can fetch the latest block from this contract. You can basically create this object EVM address from Voo. From it, we can query for balance, nonce code, code hash, all of those things.

**Ramtin Seraj**: 
And the last functionality we added for any EVM address on the EVM side, you can deposit flow token. So your flow token from the cadence layer, just like flow token vault, you pass it to this function. And on the EVM side, you can see the balance of that EVM address gets updated.

**Ramtin Seraj**: 
The other functionalities, the three other functionalities that we add here, The first one was run. As I mentioned, we want to make sure the EVM ecosystem doesn't make that much changes before. Deploying the EVM run is basically runs an EVM transaction in different formats that are available. I think there are five types of transaction formats. And the Coinbase was like something we added later on to make sure that we can have node software that can facilitate this journey.

**Ramtin Seraj**: 
And as discussed, based on the feedbacks, we added this object result, which can capture what is the state, what's the error code, how much gas was used, and everything that you need to know about executing a transaction on the ESI. If successful, then there would be a block construction, there would be corresponding events that people can follow and they make sure that this thing has happened. We've already two variations.

**Ramtin Seraj**: 
Dry run was a similar thing, but it's heavily used for running through a scripts, which you can do estimation on the gas that is used or like other purposes to make sure somethings can be run or without running it. And the last one, which we spend a lot of time on it, is batch run, which you batch a lot of transaction together. You run these things. This is not just like a for loop you call run with this transaction.

**Ramtin Seraj**: 
It's actually optimized to be very fast and provides like all the functionality that we need. Up to this point, based on the early results, it's like times to 15 times faster than just doing a true loop. So it's just way more optimized to do this. The second type of interactions in this flip that you can read more about it, is the EVM calls to cadence environment. This was very tricky because the EVM environment is not designed to be extendable, right?

**Ramtin Seraj**: 
It was even like, originally it was started with like having different opcodes, later on it's moved to support pre-compiled contracts, but there are limitations on the pre-compiled contracts. For example, one of the limitations on the implementations are they assume that it's deterministic, it's always deterministic and it's not stateful. Some functionalities that we had to adjust to make sure it's working.

**Ramtin Seraj**: 
But the only way we figured out like we could do this is was by extending the AVM side and flow to have some other AVM smart contracts that are connected to the cadence side. To test this, initially, we start building the flow block height, which we termed like a flow block number. To the EVM side, later on, we added this verified COA ownership proof that I will talk briefly about this later. Which was something we realized was necessary, must have, because there are some functionals that need this, but it doesn't stop here.

**Ramtin Seraj**: 
This is where we are going to expand and allow EVM to call into cadence. There are some limitations because of the way it is described. EVM is more limiting in the term. How it handles the data. So not everything is possible to do this. We cannot provide a lot of generic things, but it was something that we started doing this and we see this as a way of giving calls back to the cadence environment in a single transaction.

**Ramtin Seraj**: 
There are definitely like multi-step approach that you can do. For example, Cadence puts something there, AVM then can read. All of those things get cannon blocked, but if you consider that there is only a single AVM transaction that wants to load something and do something there, then this is one of the paths that we figure out during this flip. The last one was, we realized the first two might be sufficient to do a lot of operations, but From user experience, we might expose something that exists in both sides of the environments, which can facilitate a lot of operations and can make the life of the developer way easier.

**Ramtin Seraj**: 
So COA was basically a native, like there was variations of COA. This is the final version in this draft, but COA as of now is an EVM smart contract wallet type. You can think of it that way, that allows a cadence resource to own and control that EVM address. So this COA has two sides. One side, on the cadence side, there is a resource type called COA, that whoever has that resource can act and control an EVM address.

**Ramtin Seraj**: 
From that side, you have access to these things. So that's why you can create these COA resources. And then when you have a serial, you can ask for its address, you can deposit token to this, we can withdraw some token from it, from that address, which is basically deduct that balance of that account and then give you the flow vault on the other side. You can do the call. Call is very similar to the transactions, but you don't need signatures.

**Ramtin Seraj**: 
Because anyone who is holding that resource already has security parameters, there is no need for signature, just like you provide the intention of why you want to do this transaction without going through all of the signature. And there is no key here involved, right? There is no public key for the COA address. And then later on, we have also deploy, so your EVM address can deploy all of this. This is from one side, from the cadence side.

**Ramtin Seraj**: 
From the EVM side, the COA is a smart contract that supports a lot of ERC7, ERC standards. For example, you have some for like checking signatures under like the ones that it was later on added to this pile was ERC1271.

**Ramtin Seraj**: 
And all of these things are needed because from inside the EVM ecosystem, most of the time the way you handle addresses is either they're like EOA addresses, externally owned addresses, there's a public key or something like that, or it's a smart contract address. And if it's a smart contract, there are specific ERCs that you expect from it to happen or do these things. We spent a lot of time hashing out the details of how this smart contract has to look like, And eventually, we end up with this set that this is something that can unlock a lot of applications on the AVM side.

**Ramtin Seraj**: 
The TLDR is whenever you create a new COE ads account, you will receive a resource on the Cadence side, which provides a control over an address. The address would be allocated by the network, and then you can control it from the COA side. And at the same time, this COA, this address is actually a deployed contract on the EVM, which supports these ERC standards. There's more details about this in the flip, but that was where we landed with the COAs.

**Ramtin Seraj**: 
And we believe this can facilitate a lot of applications, which it's already doing, right? Bridging NFTs and like fungible tokens across two environments right now is possible because of the COAs. These were three things I discussed, but the flip stops here, but the work has been moved to other aspects as well. So there's EVM gateway flip that is already there, and there's this bridge that I discussed as follow-up of these things.

**Ramtin Seraj**: 
But this is a short summary of where we land, of how to integrate these two environments, right? I don't really have time to just like go into a lot of all of these, but it's just a summary of like where we are standing right now and where these flips are there. And then what's left. For future flips, right? We have to stop at some point and say, like, this is a package of what we deliver, and then there are these rooms for future improvements.

**Ramtin Seraj**: 
One of them is definitely expansion of cadence arc, right? What if you want to make it like a call into more generic methods on the cadence side? We build this channel to exist, but we have to think about what other functionality you want to add to this. At the same time, we have to also question, like, is it something that we cannot do through this? Because, like, as it mentioned, the eventual goal is, like, that they can access, like, an infrastructure layer that people can build cadence logic on top, right?

**Ramtin Seraj**: 
So, ideally, it requires less interaction, like here, but There are some cases that we still need to define how these two layers can talk to each other to facilitate the vision that they share. And that's something, because that can grow big in its own flip, that we left it out from this flip. We just provided two functionalities, and I think it's actually the third one is also under development and might be added to this flip or already added to this flip, which is like revertible randomness, which is another thing that we have access on the Cadence side.

**Ramtin Seraj**: 
It's very helpful on the EVM side, but that's something. But at the same time, if there are any other ideas, what are the things we are missing? From all of those goals that I described, this is what we achieved so far. And we can expand this with future flips and discussions. With this, I want to open up. I don't know how much time we have, but we can discuss about, we can have questions and we can discuss about all of those things.

**Ramtin Seraj**: 
But I will pass it to you, Alex.

**Alex Hentschel**: 
Oh, thank you. Thank you. I don't know. Do you want to take over or continue from here as the as the emcee or? Yeah.

**Dieter Shirley**: 
Well, I mean, let's just see if folks have have questions. I think it'll be obvious from the question who is best to answer it. So I think I think either you or I can take questions. If anyone has any questions or thoughts, you're welcome to put up your hand so you can ask it live or you can type it into the messages if you have any questions or concerns. The goal of my presentation and Ramtin's presentation was to make sure that everyone sort of understood that, you know, what is, you know, why and what are we planning here?

**Dieter Shirley**: 
But I think the critical aspect that Ramtin talked about is like, where are we gonna go from here? And that, you know, I'm really excited about the idea that EVM can call back into cadence. It's also an area that's like really It's fraught from a security standpoint, which is why we didn't want to put it into the first version. Question from Tom. Transaction throughput on the EVM side? Transactions per block?

**Dieter Shirley**: 
Yes, only per block. So the way that flow works is that there is no computation limit for block.

**Dieter Shirley**: 
A block can get, there's a computation limit per transaction. I don't think there's a transaction limit per block. I mean, I guess there probably practically is in that there's only so many collections and only so many transactions in a collection. Alex, it sounds like you know this.

**Alex Hentschel**: 
Yeah, we have various limits to sort of prevent a block from getting too massive, but it essentially all boils down to a transaction has a certain amount of capacity it can utilize, right? And you can pack a certain amount of transaction into a block through various mechanisms and that sort of limits the overall block resource consumption.

**Dieter Shirley**: 
Yeah, so there is a limit. It's very large. And because of the way that flow is architected, it is resilient to blocks taking too, quote unquote, too long to execute. And it'll just defer the time to seal. And that's sort of expected.

**Dieter Shirley**: 
If you look at the computation limit per transaction and you look at the ratio of gas to computation limit, I believe it's 30 million gas per transaction.

**Dieter Shirley**: 
Now, there's actually some overhead, so it's a little bit less than that, because there's some cadence code running before we get to the EVM side. But that is very close to the EVM block limit.

**Dieter Shirley**: 
A single transaction in flow can more or less do the same amount of work as a block in Ethereum. But that block would, you know, that transaction would probably take a reasonable amount of time to execute. I don't know if we've actually benchmarked it, but I think we've, we've estimated somebody, I thought somebody, I don't know, Jan, do you remember this?

**Jan Bernatik**: 
Yeah, I think we unlocked him.

**Janez Podhostnik**: 
So for reference, flow transfers.

**Janez Podhostnik**: 
With flow transfers, we can reach 600 DPS, and with flow transactions that do one EVM transfer, we can reach 450 DPS. If we throw those EVM transactions in a batch, if we do 100 transfers per flow transaction, we can reach a TPS of 60 flow transactions. So that would be like 6,000 EVM transfers. So those are just some numbers. One thing to mention is that we can fit 50 million EVM gas in a flow transaction.

**Janez Podhostnik**: 
That was the last number we decided to go with. But yeah, that's excluding cadence overhead. So realistically, it would be less than 50. Yeah.

**Dieter Shirley**: 
Any other questions, thoughts, concerns?

**Vishal Changrani**: 
Yeah, Vishal. Not a question, but I'm just kind of amazed of what we have accomplished like this. To me, this seems like a big PhD project to have like EVM sit right next to Cadence and actually do like all of this. So congratulations. This is like, this is huge, in my opinion.

**Dieter Shirley**: 
Yeah, I think it's pretty magical. I think it was really wild to see the demo where, I think it was Gregor, I can't remember. There was a demo where someone just used, what was it, Remix, and just hooked up to Flow and just started using Remix and deploying smart contracts, having these smart contracts and stuff. It's really wild. It's one thing to write that all down on paper, but to actually see it all working is really remarkable.

**Dieter Shirley**: 
So I look forward to seeing additional interesting ways of combining EVM and cadence in the future. I think we could blow some people's minds with what's possible now. And I look forward to seeing that rollout.

**Dieter Shirley**: 
Well, I think we're pretty much at time. So if anyone thinks of anything after this, please weigh in on the flip. It's 2.25.

**Dieter Shirley**: 
And this is sort of the final step before we We close this as accepted. So if you have any concerns or know of anyone who might have any concerns and wants to raise them, please make sure that happens quickly. But we will assume that folks are looking forward to this unless we hear otherwise. So we can look to this flip being merged very shortly.

**Dieter Shirley**: 
All right, thanks, everyone, for showing up. And thank you so much for your presentation, Ramtin. Have a great day, everyone.

**Ramtin Seraj**: 
Thank you. Thank you.


Meeting ended after 00:49:42 👋
