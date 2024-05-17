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

*This editable transcript was computer generated and might contain errors. People can also change the text after it was created.*

**Dieter Shirley:** I'll try not to take too much time. This will be a bit of a repeat and there won't be anything alarming or surprising but I just wanted to before we headed off to Ramtin's talk about the details. I just wanted to talk about what are sort of intentions were and our thought processes were in coming to evm on Flow and sort of why it maybe look the way it looks and what our thinking was in shaping at the way we shaped it. So, on evm support is something that we've heard from a lot of people when we go to sort of web free conferences generally talk to the web 3 ecosystem. Generally a lot of people are very interested in flow and what we're doing over here, but they have an investment in evm infrastructure.

**Dieter Shirley:** So it's something that we looked at we wanted to have support for a really long time. But there were some sort of design goals that we weren't willing to give up. And the first one was this notion of evm equivalent. So that term first came from the optimism team and the idea is that it can't just sort of run solidity code because people have an investment in code and infrastructure and a lot of that code has been audited it's been battle tested that infrastructure has existed for a while that unless it works exactly the same way that aetherium works up to including, the apis you're talking to exactly How much gas is being spent on things then there's a risk that you can't Deploy on that platform because some subtle Behavior will be different and the things that made your thing secure or correct will no longer be true the example from optimism was that they

**Dieter Shirley:** they transparently Bridge the native token to an erc20 so that when you didn't ERC 20 transfer of their native token, it would update your native balance. I'll stop talking Because unless the details of EDM this isn't going to make any sense. But the point is that they try to do something clever to make things easier and it broke an assumption of some smart contracts and by breaking that assumption those smart contracts were no longer secure so we knew that sort of runs, at Cross compiles That wasn't gonna solve the problem that people actually wanted solved which I can adopt this platform without having to rethink my code or my security model.

**Dieter Shirley:** the second thing that we were unwilling to give up on was composability with cadence there was no way for me specifically but I think the team in generally were going to have a world where the Cadence world and the evm world weren't friends that they didn't talk to each other that they didn't interact with each other because that kind of defeats the whole vision of flow which is about composability. It defeats the whole value of having, additional applications and assets being deployed on Flow if they don't work nicely with the other applications and assets that are already deployed on Flow. And the last thing we wanted was to put a bunch of effort into evm and then have evm not be cross-compatible with cadence and have the evm maybe just end up being a checkbox feature rather than something actually useful to people or the evm, getting a bunch of utility and then the kids applications feeling like they're sort of

00:05:00

**Dieter Shirley:** out of this thing. So neither side could be an island there had to be connected.

**Dieter Shirley:** and the final thing is that we wanted to make sure that even if you came to flow with an evm project and you had all this evm infrastructure that you could get access to the features some of the features of flow that were most proud of obviously Cadence is a big one but our account model and how we manage ownership and how we manage access into the U key cycling and use secure Enclave all that sort of stuff there. a lot of the value of flow comes from those features that if it weren't open to evm projects, there's kind of very little value in coming and running your evm project on Flow if you can't get access to those features, but many of those features are

**Dieter Shirley:** Are because we fundamentally broke assumptions that For example, one of the assumptions in evm is that you're account address is your public key and we broke that and so

**Dieter Shirley:** When you look at this list and I literally said this for a long time because people would ask me let's do evm on Flow and I would say look these are the things that we can't give up on and it's impossible to do evm on flow without this and it's thanks to rampton and a bunch of brainstorming and work we did together, but I have to give credit to him that we came up with this idea of baking the evm as a virtual machine sort of Docker into Cadence that we realized that we can sort of have our cake and eat it too.

**Dieter Shirley:** And so the conceptual design is that the evm is inside Cadence you can think of it as a smart contract. There's a smart contract inside Cadence that emulates the entire evm. And when you're an evm client we put these machines up called gateways that talk this sort of normal Json RPC that ethereum notes talk and they transparently wrap that coding, the transactions provided In Cadence or the state queries In Cadence scripts, but then they can see into the evm environment this limitation that evm clients can only see the evm environment is it I don't think there's any way to break that down the nature of cadence and the Cadence environment is more expressive more complex has more Dimensions than evm does and trying to represent Cadence inside evm is

**Dieter Shirley:** More or less impossible. I kind of think of it I don't know if anyone's ever read the amazing short story flatland, but it's this idea of what would it be like to live in a two-dimensional World in a three-dimensional guy goes and starts talking to a bean that lives in a two-dimensional world and I kind of feel like Evm has one less Dimension than Cadence and so we can evm into the Cadence environment, but we can't map Cadence into the evm environment.

00:10:00

**Dieter Shirley:** Cadence on the other hand sees everything right Cadence can see evm it can talk to evm it can understand all of the internals of evm. And so if you're in Cadence you get all of evm, but you also get all of cables. The other important thing that we did was to support cross VM token transfers. So, more complex objects in Cadence can't be represented in more complex smart contracts inside the evm they can be talked to from Cadence, but you can't really represent them as Cadence data types, but ERC 20 and ERC 721 the fungible non-functionable token standards on ethereum. Matt can map more or less to the fungible token standards and non-functional token standard on inside Cadence. And so what we've done is actually build a mechanism so that you can transfer tokens from one side to the other and so assets that are defin.

**Dieter Shirley:** can more or less be bridged to the other side and so

**Dieter Shirley:** If you deploy an evm token, it works in all of the Cadence smart contracts without those servant card tracks making any changes at all if you deploy an nft on the Cadence side and that nft can be a bridge into an ERC 721 smart contract on the ethereum side and evm only code can understand that so that's a really critical aspect of that composability. Then Cadence accounts actually own evm accounts, and it's actually a one to many so it's not a mapping. It's an ownership. And so your Cadence account can own a theory of addresses It won't always be the case you'll do that. But as if you're a developer, it can be very handy to potentially have multiple evm addresses and then the other mental idea that I want folks to keep in their mind. Is that one way especially as a developer that you can think about the way Cadence talk to each other.

**Dieter Shirley:** Is that Cadence is evm almost the same as rust is to see So if there's a library that does what I need, I'm a rust developer. There's a library that does what I need. It's written in C. I don't have to rewrite that library to use it in my rest application. I can just take that c code wholesale and put it inside my rest application. if now

**Dieter Shirley:** the reason I use C and not some other language like go or python is because the example of Rustin C the example of cadence and evm, there's very little in the way of efficiency Improvement. if you wrote python code you might want to intentionally write C code for performance Reasons from your python. That's not the case and I hope no one thinks that way about writing coding evm. we're working very hard to make sure Cadence is highly efficient. There may be situations today where evm is a little bit more efficient than Cadence but we're gonna be putting a lot of effort into improving the efficiency of cadence and I don't think that same effort is gonna go into evm side because we're drafting off of the evm implementation from the ethereum community. This is not a net new evm implementation. We are using the code directly from death. And so

**Dieter Shirley:** I would expect to see the Cadence logic will get faster over time. Whereas evm launching will probably not speed up. So I would encourage you to use Cadence for new code. But if you have existing code in the evm that you want to leverage by all means make use of that. so

**Dieter Shirley:** I think it's useful to think through three different personas in terms of how they're going to interact with evm on Flow and how they might think about it differently. So the first Persona are cost cross-chain infrastructure providers, projects who are inherently interacting with multiple blockchains and it's fun to mental in there functionality. the next group we'll talk about is the people who are building evm based applications that have some sort of, I don't just mean consumer facing as in it's a game or something like that. I can be defiring like that. But where end users are using it directly often these infrastructure providers, they're developers. This is where you're providing functionality and users. And then of course Cadence app developers is a very important group and I want to talk about how they should think about.

00:15:00

**Dieter Shirley:** Evm as well.

**Dieter Shirley:** So cross Gene infrastructure for the most part. They don't even need to think about the Cadence side of things. They can just talk to flow as though it's an evm chain and depend on the fact that all of the token Bridge the ability for Cadence to see inside the evm and to call code inside the evm whatever infrastructure they value they provide to the chain will be by making it available to evm. They are making it available to Cadence without any extra work on their part and I give some example here price oracles feeding data into the evm. You'll be able to see that from Cadence Bridges bridging tokens from other chains into our evm. those things can be Bridge back into Cadence centralized exchanges, the ability to deposits and withdrawals directly on chain if they choose to go evm only for that integration because that makes their lives easier. that's fine because if you have a flow reference wallet

**Dieter Shirley:** or some are fcl wallet, you can still interact with those centralized exchanges and cross-chain Dex is as well. you can sort of think of them as crashing infrastructure. They're kind of a mix because they also tend to have a direct user facing but if you are working cross-chain, you probably already have to dip your toe in metamask. And so the fact that these kinds of applications may only work with metamaskis is probably fine and so in terms of cross-chain infrastructure, it's kind of the best that both worlds where the cross chain infrastructure team who typically already have the ability to support evm chains can just flow to their list of supported chains, but all the Cadence developers get all the benefits of having a chain. We're building on a chain that has that infrastructure available to it.

**Dieter Shirley:** On evm apps if you're an evm dap developer and you want to deploy on Flow if you're okay restricting your users to metamask.

**Dieter Shirley:** You're good. You just Deploy on Flow and it just works Caden funds will touch in tokens Can Be breaching to that EDM environment and your evm only application can work with all those assets even though it only works with metamask, but where I get really excited is evm Dabs at some point in time in the future and this could literally be right, the day after it could be months later, but they can As needed as desired starts to add flow specific features without having to rewrite and disrupt their existing functionality. So a lot of flow features like abstraction secure Enclave account linking transaction batching those can be accessed through Cadence.

00:20:00

**Dieter Shirley:** But by only changing their off chain user interface code. So if they have chain infrastructure code backend code that's like indexing the chain or something like that. Then that code never needs to understand Cadence. If they have a smart contract where all of their logic lives inside evm that can stay they never have to deploy additional smart contract functionality all of these features that you see here that can all be done on the front end and they can be in a situation where they're working with flow reference wallet. they're using flow action Cace transactions are using Cadence scripts all to create their UI. they haven't deployed a single line of Cadence as a smart contract and that gives them access to all of these features. They're still using the same smart contract code they had before on the other hand. You want to add new features to their smart contract. They can wrap the existing evm spark contract in a Cadence smart contract and that's where that rust to see analogy comes in. You can have this game smart contract where

**Dieter Shirley:** If it's not new effect functionality great you just call into the evm and have the evm do its thing if it's new functionality and you think it'd be better represented in Cadence. Then you write in Cadence and to code outside It can talk to that Cadence smart contract without even knowing that evm exists on the inside and it allows those evm depths to become full Cadence apps with all of the advantages of that without ever having to go through a step of rewriting anything.

**Dieter Shirley:** Cain stops on day one I think is the same story right if you're okay working with fcl while it's including the flow reference wallet, which is going to support both fcl and web 3, then you don't have to do anything all of any assets that could deployed on the evm side of things can come over and can be used whether it's fungible focus is not fungible tokens. Those can be used inside Cadence. You don't have to do any work at all because we're putting the work into flow reference wallet to support web 3 People who want to use Cadence apps and in any of those evm daps that haven't done the extra work to support Cadence functionality if they use flow reference wallet, they get the best of both worlds and they don't have to give up either side.

**Dieter Shirley:** On the other hand some Cadence apps might choose to add support for and I say metamask, but what I mean is any sort of, ethereum style web 3 wallet and at first this might seem impossible right? It's like you can't ask minimask to sign a Cadence transaction. So, how can I get metamask to talk to my kid in the smart contract and it turns out that there's a pattern. It's really common in the ethereum world, which is doing approvals and user sign rather than direct transactions and the flow World. We're often we say the user. Hey,

**Ramtin Seraj:** Check State. Let me share my screen.

**Ramtin Seraj:** Let's see this working. Click here. It's not sure this is nice. Yeah. Thanks for the introduction and motivation. I can skip definitely view slides and I would be happy to do that. So today I'm going to presentation of this flip 225. Which is evm compatibility. And I'm really excited for that. But before I jump into that I want to thank Every one…

**Dieter Shirley:** We want to do this complicated thing that uses lots of different smart contracts lots of different assets,…

**Ramtin Seraj:** because the state of this flip right now is very different from the original one that we drafted.

**Dieter Shirley:** but you can do that from one transaction. The ethereum model actually makes that very difficult. And so it's very very common for you to go to a trading platform whether it's for fungible or…

**Ramtin Seraj:** And the reason for that is because we continue to receive a lot of feedback from the community.

**Dieter Shirley:** non-functionable tokens and…

**Dieter Shirley:** I delegate you smart contract the ability to move my assets around and…

**Ramtin Seraj:** We were fortunate to be able to run this on preview net.

**Ramtin Seraj:** We had a really

**Dieter Shirley:** then later when I want to do a trade I do a user sign sometimes called off-chain message signing.

**Ramtin Seraj:** Good community and…

**Dieter Shirley:** I do a user sign and…

**Ramtin Seraj:** then they supported us to do fast iteration great things experiments as we explore these things…

**Dieter Shirley:** I hand not a trans signed transaction, but assign data blob to that smart contract and…

00:25:00

**Ramtin Seraj:** because this was not something that was done before it was very new.

**Dieter Shirley:** then I trust it's logic to it's this second kind of authorization mechanism to go and…

**Ramtin Seraj:** It was a lot of time areas of uncertainty. We didn't know if this is gonna work or…

**Dieter Shirley:** move my assets as expected.

**Ramtin Seraj:** not and then Thanks to all of…

**Dieter Shirley:** Right? This is the way unit swap works.

**Ramtin Seraj:** I will present…

**Dieter Shirley:** This is the way open to see works.

**Ramtin Seraj:** what you all has achieved with this flip.

**Dieter Shirley:** It is a very common pattern in some cases.

**Dieter Shirley:** The only way to do certain kinds of Trades and in other cases, it's frequently used because it's more efficient right? You can combine multiple user sign blobs into a single transaction and

**Ramtin Seraj:** we can escape the motivation you should by now be highly motivated after this talk the main question for this flip…

**Ramtin Seraj:** because there was discussions of the AVM compatibility in the Forum and all of those things that the main question for this really was how to integrate As it mentions there was we want to make sure we have higher level of composibility between two environments. We can have Atomic operations across the environments. We want to have another message passing across messaging like bridge between two chains or any approach like that. We want to make sure it's to make calls our support at this. we wanted to minimize the change required for tooling on both ecosystems.

**Dieter Shirley:** You can sort of get the efficiencies of batch operations by using these there's no reason…

**Ramtin Seraj:** We didn't want to just have breaking change in both sides and assume they have to do a lot of things and…

**Dieter Shirley:** why you as a Cadence app developer can't create a COA that is owned by your smart contract a metamask user grants approval to that COA.

**Ramtin Seraj:** the last one is It seems obvious. But sometimes you have to mention this we didn't want to sacrifice and safety security measures or Primitives on each of these and environments. and…

**Dieter Shirley:** So from their perspective, they're just granting an ERC 20 or…

**Ramtin Seraj:** that was very challenging and…

**Dieter Shirley:** ERC 721 approval to that address and…

**Ramtin Seraj:** the reason is spiritual challenging is both Cadence and evm are Fundamentally different environments.

**Dieter Shirley:** that address is controlled by a smart contract and…

**Ramtin Seraj:** They're different in many ways that programming models clearly like you have resources on one side.

**Dieter Shirley:** then you can do the same kind of logic that openscene in uniswap to where they look at an order and see if it's correctly signed. You can do that logic inside Cadence.

**Ramtin Seraj:** The other side's different the account and…

**Dieter Shirley:** You don't do that logic inside EDM…

**Ramtin Seraj:** data models are very different you have a letter style of for example ownership tracking on one side.

**Dieter Shirley:** if you want again, there's lots of examples of doing that and so if you want to leverage that evm code you can do that.

**Ramtin Seraj:** The other side the echo is actually hold on to things.

**Dieter Shirley:** But critically the point is that…

**Dieter Shirley:** if you support web 3 in your HTML page and…

**Ramtin Seraj:** Resource consumption metering and…

**Ramtin Seraj:** a storage pricing completely different than both environment.

**Dieter Shirley:** you use the model of approvals and…

**Ramtin Seraj:** You have gas metering an evm size and…

**Dieter Shirley:** user sign which

**Dieter Shirley:** most ethereum users are highly accustomed to

**Ramtin Seraj:** the Cadence you have this notion of computation. And the way that they meter is very different storage pricing is really different. You have minimum balance on the Cadence side. I need to just one-time fee of gas, which is the motorbike that you're changing security Primitives is very different or Access Control capabilities. I do the Hillsborough of those things and then also even a higher level once the standards for example the way that you keep a balance or native token balance on ethereum or…

**Dieter Shirley:** You do not need to deploy a single line of EDM code in order to work with metamax.

**Ramtin Seraj:** like blood sorry and all of the evm chains, it's Orion and other ones they have different precisions or have different standards or NFD have different standards. So It was challenging …

**Dieter Shirley:** You do need to do some evm indexing.

**Ramtin Seraj:** how to integrate this. That was the main question and…

**Dieter Shirley:** I won't get into the details of that here your Cadence smart.

**Ramtin Seraj:** the main question that this flip tried to answer. So some of the core decisions just like some of them…

**Dieter Shirley:** Sorry your Cadence transactions will need to understand EDM…

**Ramtin Seraj:** because I did mentioned some of the other ones but the very first decision that was there is just idiom should use flow as its own native token.

**Dieter Shirley:** because they need to call into evm to do some logic there. But you don't need to deploy new smart contracts.

**Ramtin Seraj:** We don't want to meet a new token.

**Dieter Shirley:** You just need to understand enough about the evm in order to do this approval and…

**Ramtin Seraj:** We want more utility with the current ken. And any token that is on the evm side should be breached from the kitchen side.

**Dieter Shirley:** user sign flow. And so you can keep the vast majority of your code the vast majority of your effort can be inside Cadence and…

**Ramtin Seraj:** And the second important was as Dimensions Cadence was to act as a main point of entry.

**Dieter Shirley:** But you can still add support from edms.

**Ramtin Seraj:** So we want to reuse the flow transaction format. We didn't want to break that thing or introducing new transaction type which means the decadence has to wrap everything about evm and provide all the utilities there at the same time. If we do you use the same format of flow and flow transactions and do this wrapping. We want to have the unified resource consumption which means gases to convert into computation and then same settlement environment and all of those things. So it's easier to understand how things are working. And also if you consider cases the main point of entry then we can have Atomic operation across environments because it's like single thing that can.

**Dieter Shirley:** I honestly can't tell you whether or…

**Dieter Shirley:** I think that's a good idea.

**Ramtin Seraj:** basically wrap it all the functionalities and…

**Dieter Shirley:** I don't know whether or not we're going to see a lot of users coming with Ben.

**Ramtin Seraj:** The likes and…

**Dieter Shirley:** I'm asking interacting with flow and be desperate to use Cadence applications and…

**Ramtin Seraj:** support Atomic operations, which is very helpful for the bridging acids…

**Dieter Shirley:** won't be open to using flow reference wallet instead.

**Ramtin Seraj:** a lot of other operations that I will tell later and the last one was like…

**Dieter Shirley:** If you take a look at Solana,…

**Ramtin Seraj:** which we added a lot of these things.

**Dieter Shirley:** everyone's very comfortable using this wall house Lana specific wallet,…

**Ramtin Seraj:** I'm talking it was added over time by the feedback. We wanted to make sure the Cadence logic has full control over outcome of executing a trend like evm transaction.

**Dieter Shirley:** but if you look at a lot of other, evm compatibility change, they all just use metamask,…

**Ramtin Seraj:** For example,…

**Dieter Shirley:** and…

**Ramtin Seraj:** if any specific error happened …

**Dieter Shirley:** certainly and then there's a projects near…

**Ramtin Seraj:** what are their codes what's the status of transaction ended?

**Dieter Shirley:** where they have sort of support from metamask and…

**Ramtin Seraj:** So they're under their overarching Logic on the Cadence.

**Dieter Shirley:** but it isn't exactly equivalent so I don't know exactly

**Ramtin Seraj:** I can decide how to behave in case of running a transaction or…

**Dieter Shirley:** To fall in I think that's got to be up to you as an Cadence app developer,…

**Ramtin Seraj:** something failing because of the sequence number or something is failing…

**Dieter Shirley:** but I just want to make sure that there's a path there and…

**Ramtin Seraj:** of other factors, the territorical part of the Court decision was like EVMS deploying as a ritual chain,…

**Dieter Shirley:** if you choose to adopt that on day one, we would want to help you and…

**Ramtin Seraj:** which would discuss Which is we deploy?

**Dieter Shirley:** if you want to take a wait and see attitude and see how many metamask users come in.

**Dieter Shirley:** I also think that that makes a certain amount of sense and…

**Ramtin Seraj:** Evm as a Cadence smart contract language that you can import other smart contracts.

00:30:00

**Dieter Shirley:** you can always add this functionality in later just by changing your UI.

**Ramtin Seraj:** Though we realize that we need some privilege underlying access…

**Dieter Shirley:** You don't have to do anything on chain.

**Ramtin Seraj:** because there are some functionalities and evm that you need more access for or you need a different way of interacting with the hardware. So that's the reason this is smart contract will it's an idiom smart contract but it has access to some functionalities that is basically implemented in natively and that can gain a lot of performance and…

**Dieter Shirley:**

**Dieter Shirley:** Okay so that took longer than I expected.

**Ramtin Seraj:** a lot of

**Dieter Shirley:** Rampton. I hope you can fit your stuff in…

**Ramtin Seraj:** Other factors, but in theory,…

**Dieter Shirley:** but I just wanted to make sure people sort of understood…

**Ramtin Seraj:** it should be as if we completely reimplement evm In Cadence,…

**Dieter Shirley:** where we were coming from when we did evm and…

**Ramtin Seraj:** which we didn't do for performance reasons.

**Dieter Shirley:** to think about…

**Ramtin Seraj:** So block progress it's basically trackable through Cadence events.

**Dieter Shirley:** how various parties fit into that. the one thing I wanted to mention.

**Ramtin Seraj:** So every time be a black evm block is moving,…

**Dieter Shirley:** You all shouldn't be surprised…

**Ramtin Seraj:** then you can follow the chain of events and…

**Dieter Shirley:** if you see people that currently support flow.

**Ramtin Seraj:** you have proofs for that you have inclusion proofs and all of those things. It was another recession. Even transaction basically as I mentioned is about to inside the flow transaction. So even from evm tooling perspective, they can reuse their Legacy or other forms of transactions that are supported by evm readout the need to know anything about flow or introducing new types or anything like that. and then we spent a lot of time thinking about several ways of cross environment interactions. Obviously the first one. Which is used by some other platforms was ruled out for us, which was shared memory access between two environments.

**Ramtin Seraj:** Cadence has this higher level of safety measures that we didn't want to jeopardize by providing raw memory access or anything like that. So we opting for cross calls in a way that we can cover as much as applications as possible and The unit is flip.

**Dieter Shirley:** And have cross-chain infrastructure and…

**Ramtin Seraj:** It came up with three ways of communications between these two environments.

**Dieter Shirley:** there's a number of projects that do this actually switch to the evm side of things so that their maintenance effort is easier,…

**Ramtin Seraj:** The very first one is So Cadence can see everything I mentioned there's an evm smart contracts.

**Dieter Shirley:** So right now they're often implementing two code paths, They have a code path for all the evm chains and…

**Ramtin Seraj:** So you can fetch the latest block from this contract.

**Dieter Shirley:** then they have a Cadence path for supporting flow.

**Ramtin Seraj:** You can basically create this object evm address from its weekend query for balance notes code code hash all of those things and…

**Dieter Shirley:** Some of those teams will choose to keep the Cadence side running. Some of those teams will switch to evm. We've told them that we're comfortable with either that flow gets the benefit of their support regardless of…

**Ramtin Seraj:** the last functionality we added for any evm address the evm side. You can deposit flow token.

**Dieter Shirley:** which side that they're on and…

**Ramtin Seraj:** So your flow token from the Cadence just flow took and…

**Dieter Shirley:** so please don't see it as alarming…

**Ramtin Seraj:** Vault you pass it to this function and…

**Dieter Shirley:** if you see somebody switch to evm, especially with the cross chain infrastructure.

**Ramtin Seraj:** on the evm side, you can see the balance of that EDM address gets updated.

**Dieter Shirley:** There's literally no reason for them to try and maintain both sides.

**Ramtin Seraj:** The three other functionalities that we had here.

**Dieter Shirley:** So I think we'll see a lot of both new teams coming into to flow that that haven't been able to

**Ramtin Seraj:** First one was run as I mentioned. We want to make sure the evm ecosystem doesn't equal that much changes before deploying. The even Brown basically runs an evm transaction in different formats are available.

**Dieter Shirley:** Lies the extra expenditure of having another code base. We'll be joining us…

**Ramtin Seraj:** I think there are five types of transaction formats.

**Dieter Shirley:** but also teams sort of moving into evm…

**Ramtin Seraj:** And…

**Dieter Shirley:** because that makes their future maintenance easier.

**Ramtin Seraj:** the coin Visa was like something we added later on to make sure that we can have notes software that can facilitate this journey.

**Dieter Shirley:** Please over to you ramtin and there will be time for Wow,…

**Ramtin Seraj:** and as discussed based on the feedbacks,…

**Dieter Shirley:** and now that I'm taking up there might be some time for Q&A about this later,…

**Ramtin Seraj:** we added this object result…

**Dieter Shirley:** but I want to make sure ramtin has a chance first.

**Ramtin Seraj:** which can capture …

**Dieter Shirley:** So take it away ramtin.

**Ramtin Seraj:** what is the state was the record was how much gas was used and all everything that you need to know about executing a transaction on the union side if successful then there would be a block construction there would be Corresponding events that people can follow and they make sure that this thing has happened before a two variations dry run was similar thing, but it's heavily used for running through scripts which you can do estimation on the gas that is used or other purposes to make sure something's can be run or without running it and the last one which was a lot of time on it. It's best run which you back a lot of transaction together you run these things. This is not just like for Loop you call one with these transaction. It's actually optimized to be very fast and provides are

**Ramtin Seraj:** all the functions that we need up to this convention the early resources 10 times to 15 times faster than just doing it through a loop. So it just Way more optimized to do this the second type of interactions in this flip that you can read more about it is the evm calls to Cadence environment. This was really tricky because the evm environment is not designed to be extendable, right? originally it was started with having different up codes later on. It's moved to support precompiled contracts, but there are limitations in the pre-compiled contracts. For example, one of the replacing the implementations are they assume that is always deterministic. It's not cool and some functionalities that we had to adjust to make sure it's working but the only way we figure out like we could do this was extending the On flow to have some other evm smart contracts that are connected to the Cadence side.

00:35:00

**Ramtin Seraj:** To test this for initially we start building the flow block height, which return of a flow block number to the evm side later on. We added this verify COA ownership proof that I will talk briefly about this later which was something realized always necessary must have because there are some functions that need these but it doesn't stop here. This is where we are going to expand and low evm to call into Cadence. There are some limitations because of the way we described evm is more limiting into term how it handles the data. So not everything is possible to do this. We cannot provide a lot of generating things, but it was something that you start doing this and we see this as a way of evm close back to the Cadence environment in a single transaction. There are definitely

**Ramtin Seraj:** Multi-step approach that you can do for example Cadence put something there again, then can read or all of those things that can unblock. But if you consider there is only a single evm transaction that wants to load something and do something there. Then this is one of the paths that figure out during this flip. and the last one was realized the first two might be sufficient to do a lot of operations, but From user experience. We might expose something that exists in both sides of the environments which can facilities a lot of operations and can make the life of the lower very easier. So there was variations of COA. This is the final version in this draft. But Siri as of now is a medium smart contract wall at the time.

**Ramtin Seraj:** You can think of it that way that allows a Cadence resource to own and control that evm address. So this COA has one side on the Cadence. There is a resource type called COA that whoever has that resource can act and control an evm address. from that side you have access to these things. So therefore you can create this COA resources and when you have a series you can ask for its address. You can deposit token to this you can withdraw some token from that address, which is basically deduct that balance of that account and then Give you the flow Vault onto the other side. You can do the call call is very similar to the transactions, but you don't need signatures.

**Ramtin Seraj:** Because anyone who is holding that resource is already half secret parameters. There's no need for Signature. Just like you provide the intention of I want to do this transaction without going through all of the signature and There's no public key for the serial address. And then later on we have also So your idiom address can deploy all this. This is from the evm side. The co is a smart contract that's supports a lot of rc7 ERC standards. For example, you have some for checking signatures and they're like the ones that it was later on added to this pile was prc2l71

**Ramtin Seraj:** and all of these things are needed because a lot of Echoes from inside the evm ecosystem most of the time the way you handle addresses is either they're like eoe addresses externally own addresses. There's a power public use something like that or is a smart contract address and if it's a smart contractors or a specific ERC is that you expect from it to happen or do distance. We spend a lot of time hashing out the details like how this smart contract has to look like And eventually we end up with this set that this is something that can unlock a lot of applications on the evm side. The tldr is whenever you Create a new series account. You will receive a resource on the Cadence side.

**Ramtin Seraj:** Which provides a control over an address and address would be allocated by the network and then you can control it from the series side and at the same time This address is actually deployed contract on the evm which supports these ERC standards. There's more details about this in the flip, but that was where we landed with the series and we believe this can facile a lot of applications which is already doing right bridging and if teas and fungible tokens across to environments right now is possible because of the COS. these were three things that discussed but the flip stops here, but the work has been moved to other aspects as well. So it's even get very flip that is already there. And there's this bridge that they discussed is follow-up of these things. But this is the short summary of where we land of how to integrate these two environments, right?

00:40:00

**Ramtin Seraj:** I definitely don't have time to just go into a lot of all the details basis was a summary of where we are standing right now, and these flips are there. And then what's left for future Flip's, right? What's we had to stop at some point this is a package of what we deliver and then there are this rooms for future improvements. One of them is definitely expansion of cadence. What if you want to do make it you like a call into more generic methods on the Cadence side, we build this channel to exist but we have to think about what other functionality you want to add to this at the same time. We have to also questions. is it something that we cannot do through this because as it mentioned eventual goal the max is aim for structure later that people can build Cadence on top, right?

**Ramtin Seraj:** So ideally they requires less interaction like here but there are some cases that we still need to Define how these two layer can talk to each other to facilitate the vision the teacher and that's something we like because that can grow big it's its own flip that we left it out from this flip. We just provided to functionalities. I think it's actually the third one's also. Under development and might be already added to this Felipe which is reversible Randomness, which is another thing that we have access on. The Cadence side is very helpful on the evm side, but that's something it's but at the same time if there are any other ideas, what are the things we are missing because From all of those goals that I describe this…

**Alex Hentschel:** No, Thank you. I don't know.

**Ramtin Seraj:** what we achieved so far and…

**Alex Hentschel:** Do you want to take over or continue from here as the semc or…

**Ramtin Seraj:** we can expand this with a future.

**Alex Hentschel:** ?

**Dieter Shirley:** I mean, let's just see…

**Ramtin Seraj:** Flipz and…

**Dieter Shirley:** if folks have questions.

**Ramtin Seraj:** discussions With this I want to open up.

**Dieter Shirley:** I think it'll be obvious from the question who is best to answer it.

**Ramtin Seraj:** I don't know how much time we have…

**Dieter Shirley:** So, I think either you or…

**Ramtin Seraj:** but we can have questions that we can discuss about all of those things,…

**Dieter Shirley:** I can take questions if anyone has any questions or…

**Ramtin Seraj:** but I will pass it to you Alex.

**Dieter Shirley:** thoughts. You're welcome put up your hands so you can ask it live or you can type it into the messages. If you have any questions or concerns that the goal of my presentation in ramtin's presentation was to make sure that everyone sort of understood that why and what are we planning here? But I think the critical aspect that ramtin talked about is where we gonna go from here and that, I'm really excited about the idea that evm can call back into Cadence. It's also an area that's really

**Dieter Shirley:** It's fraught from a security standpoint,…

**Alex Hentschel:** Yeah, we have various limits to sort of prevent a block from getting to massive.

**Dieter Shirley:** which is why we didn't want to put it into the first version question from Tom transaction through put on the evm side transactions for Block.

**Alex Hentschel:** But it essentially all spoil boils down to a transaction has a certain amount of capacity.

**Dieter Shirley:** Yes only for Block. So the way that flow works is that there is no computational limit for block a block there's a computation limit per transaction.

**Alex Hentschel:** It can utilize right and you can pack a certain amount of transaction into a block through various mechanisms, and that sort of limits the overall block resource consumption.

**Dieter Shirley:** I don't think there's a transaction limit per block. I mean, I guess it probably practically is and that there's only so many Collections and only so many transactions in a collection Alex. It sounds like this

00:45:00

**Dieter Shirley:** Yeah, so there is a limit it's very large and because of the way that flows architected it is resilient to blocks taking two quote unquote too long to execute and…

**Jan Bernatik:** Yet we understand.

**Dieter Shirley:** it'll just defer the time to seal and…

**Janez Podhostnik:** Yeah, we so for reference flow transfers with flow transfers.

**Dieter Shirley:** that's sort of expected if you look at the computation limit per transaction and…

**Janez Podhostnik:** We can reach 600 DPS. And with flow transactions that do one evm transfer we can reach of 450 DPS.

**Dieter Shirley:** you look at the ratio of gas to a computation limit, I believe it's 30 million gas per transaction.

**Janez Podhostnik:** If we throw those evm transactions in a batch.

**Dieter Shirley:** There's actually some overhead so it's a little bit less than that…

**Dieter Shirley:** because there's some Cadence code running before we get to the evm side,…

**Janez Podhostnik:** if we do 100 evm transfers Per flow transaction,…

**Dieter Shirley:** but more that is very close to the evm block limit.

**Janez Podhostnik:** we can reach a TPS of 60 flow transactions.

**Dieter Shirley:** And so

**Janez Podhostnik:** So that would be 6,000 evm transfers so those are just one thing to mention is that We can fit 50 million EPM gas in a flow transaction.

**Dieter Shirley:** A single transaction in flow can more or less do the same amount of work as a block and ethereum, but that transaction would probably take a reasonable amount of time to execute. I don't know if we've actually benchmarked it but I think we've estimated somebody I thought somebody I don't know John.

**Janez Podhostnik:** That was the last number we decided to go with but yeah, that's excluding.

**Dieter Shirley:** Do you remember this Greg?

**Janez Podhostnik:** Cadence overhead. So realistically it will be less than 50. yeah.

**Janez Podhostnik:** Yeah.

**Dieter Shirley:** Any other questions thoughts a concerns?

**Dieter Shirley:** Yeah Vishal.

**Dieter Shirley:** Yeah, I think it's pretty magical. I think it was really wild to see the demo where I think it was Gregor. I can't remember. there was a demo where someone just used what was It remix and just hooked up the flow and just started using remix playing spark contracts having these smart contracts and stuff. it's really wild it's one thing to write that all down on paper, but to actually see it all working is really remarkable. So I look forward to seeing additional interesting ways of combining evm and Cadence in the future, I think we could blow some people's minds with what's possible now, and I look forward to seeing that roll out.

**Dieter Shirley:** I think we're pretty much at time. So if anyone thinks of anything after this. Please weigh in on the flip. It's 225 and this is sort of the final step before we close. This is accepted. So if you have any concerns or know of anyone who might have any concerns and wants to raise them, please make sure that happens quickly, but we will assume that folks are looking forward to this unless we hear otherwise so we can look to this flip being merged very shortly.

**Dieter Shirley:** All Thanks everyone for showing up and thank you so much for your presentation, Ramtin. Have a great day everyone.

**Alex Hentschel:** Thank you.


Meeting ended after 00:49:42 👋