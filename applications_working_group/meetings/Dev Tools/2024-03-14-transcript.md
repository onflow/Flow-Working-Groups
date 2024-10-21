Dev Tools Working Group 
Thu, Mar 14, 2024

0:00 - Unidentified Speaker 
features and stuff out.

0:00 - Chase Fleming 
Is it via this or should we be doing it via something else?

0:01 - Ali Serag 
I think working groups are a great way to do user research and ask developers and community members questions about what tooling is really missing in the ecosystem, but along current themes. Right now our two biggest themes are Cadence 1.0 migration and EVM. So what kind of tooling infrastructure is currently missing relating to migration and EVM? Doing like a kind of user research, getting feedback about what developers love, what they're curious about, what they don't understand, like their pain points and use that as a way to like gather those insights and source new tools or enhancements or improvements so we can have a show and tell dynamic but it shouldn't just be like this is what we're working on you've been updated like it should have a component of cross collaboration like this is what we're working on like getting feedback on it is it actually solving people's problems and trying to come up with new tools as well.

1:03 - Chase Fleming 
Maybe in the education group then, maybe we should talk about at some point, how do we better promote our new features? Because I feel like we build so much stuff. And this has been a problem for a while. But we're so bad at letting anyone know. I love that.

1:19 - Ali Serag 
We should have an entire dedicated working group session on just that. How do we let the community know what we're working on? Because we're building, right? We ship things, but then we we need to get better at making it public.

1:35 - Tom Haile 
Yeah, I think there's definitely some crossover with education. Like, hey, here's a tutorial or whatever education on this tool that is available. And then of course, here in the tooling, it's like, hey, we have this tool that does this more specific deep dive stuff and get more user feedback, kind of makes sense. I could see the demo could fit on either side of that, but I think the higher level kind of touch point would be tutorials and, you know, readme's and all that kind of stuff. And then it could be deep, deep Devon, Devon, I'll say Devon into a demo because Devon's the new AI software engineer hotness. Going on right now if you've been following, okay You should add that to the agenda.

2:26 - Ali Serag 
Like I I still haven't caught up on grok. I still haven't caught up on google's thing Hey, welcome. Welcome.

2:33 - Chase Fleming 
It's just basically it's it's another lm but it integrates a lot of tools together so it can like If if it gets an error, it'll just keep trying to fix it and fix it in a browser until it gets it Right and that that's that's basically what it is. It has no 13 success, right? So it's not like obviously I'll get better over time, but It's basically an elementary school child learning how to develop.

3:00 - Brian Pistone (BoiseITGuru) 
I'm just waiting for the AI apocalypse, though, because they're starting to consume their own content and will just start putting out nonsense.

3:09 - Chase Fleming 
Well, humans have already been putting out nonsense.

3:14 - Ali Serag 
I'll say they grow up so fast.

3:19 - Chase Fleming 
It keeps putting out content on whatever the most popular content is, right? It's like, becomes this like compounding effect, like will react ever get replaced as the top framework anymore? Will there be more framework wars? Because it's like, there's already majority react content. So if you only create more react content, does it now? And then it's like, yeah, uh, yeah, it compounds. Greg had something.

3:45 - Unidentified Speaker 
She had something.

3:46 - Ali Serag 
Nope. Just trolling.

3:50 - Tom Haile 
We should probably do the agenda I'm gonna start recording guys.

3:55 - Ali Serag 
If anyone has any objections to that take it up with the AI, please I'm gonna remove the L for my name All right, everybody. Happy Thursday. Welcome to the DevTooling Working Group. Today we're going to be led by Tom. I'm going to start off with a quick OKR and go over the agenda and hand it over to him. In terms of OKRs, where are we at with the DevTooling working group? Our main goal this quarter is bringing Crescendo to launch. Crescendo has two major components, like we talked about last time. The first component is the Cadence 1.0 migration, essentially trying to get all the developers in the ecosystem that have launched codes, transactions, and scripts to upgrade to stable cadence, which marks our language's maturity. It has a lot of exciting enhancements from efficiency with A-tree, speed, security, readability, UX, and two new features, including view functions. And essentially, if people don't upgrade by the time it goes live, it is introducing breaking changes, so there's going to be a coded get in. So really need to make it as smooth and easy as possible for people to upgrade their contracts. And that's where dev tooling plays a very key role. How do you make it as easy and simple as possible to identify which parts of your code you need to upgrade, or help minimize the time and effort required to upgrade your code? The second major component of Crescendo is EVM on Flow. Already, we've been seeing massive improvements in growth in DeFi within Flow. There is a 180-ish percent increase in TVL from 2022 to 2023. There is a 800 percent and 930-ish percent increase in both lending and liquid staking in the ecosystem as well. Now that's going to become exponentially even more when EVM equivalency is introduced and tons of liquidity comes in from the Ethereum ecosystem as well as builders and new primitives because barriers towards building are going to be taken down. That being said, there's also a lot of opportunities to create developer tooling for all these new EVM developers that will be coming into our ecosystem to get their code launch faster, as well as for our cadence devs to transition into that EVM environment and take advantage of new business opportunities and the new market that's going to be coming in. So that's that in terms of our agenda. We're going to start off with a cadence 1.0 migration status. What are the migration tools that are available, including changes to the flow CLI? What are the flow EVM tools that we would love to see? The dependency manager which will be a little presentation and conversation by our very own chase the linter tool which is a really cool tool to help people identify code that needs to be changed for the upgrade vs code changes and I just added this at the very end a little bit of a conversation if we have time on the most useful ai tools for upgrading as well as EVM or smart contract development. So without further ado, I will hand it back to you, Tom. Thanks.

7:40 - Tom Haile 
So one of the big things which you mentioned is the contract migration tools, which I was hoping Ian would be in here. Let me present the agenda. Do we have any status on number of contracts that have been upgraded or staged? Absolutely.

8:20 - Ali Serag 
And I'm going to ask the crew here today, where would you want to go if you want to see? Actually, I'm going to correct myself. We don't have any information on the number of contracts staged. We're currently working with the data team on that. Part of the reason that we aren't prioritizing it so it happens very, very fast is because first week of April is when we're expecting the test upgrade environment to go live. So we still have several weeks. I'm trying to work with the data team to have staging tracking live before the end of this month, however. And the, yeah, the main reason is because you're only going to be able to stage on testnet initially and then eventually on mainnet. That being said, we do have something right now that is available. Does anyone want to, you know, give a guess to what that might be? We don't have the test environment available, but there is a network that people can use. Anyone? What is the cool network? It was announced during ETH Denver. PreviewNet.

9:29 - Tom Haile 
No, not contract browser.

9:31 - Ali Serag 
PreviewNet, exactly. So we can get some very interesting signals about activity and who's actively trying to upgrade their contracts based on what are the contracts that are deployed to PreviewNet and looking at some of the data there. Does anyone know how we could get visibility into that or what tool is available to get visibility into that? I'm going to guess FlowDiver.

9:53 - Tom Haile 
Yes, FlowDiver.

9:55 - Ali Serag 
So do you want to pull it up real quick, Tom? Just because I realized not a lot of people might know that PreviewNet on FlowDiver is live. If you add a prefix, like PreviewNet.FlowDiver.io, it will open up... Oh, actually, there's a dropdown at the top right there. Oh, yeah, you're already on PreviewNet. If you click on Analytics... There we go.

10:23 - Tom Haile 
Yeah, that's much better.

10:24 - Ali Serag 
Oh, shit, there's a Christmas mode still enabled. So what we see here is that in the last seven days, there's been 13 contracts that have been added to PreviewNet. There's been 28 accounts that have been created, and there's 288 active accounts and 435 transactions. If we want to see what those, ooh, maybe that 13 is not actually for the last week. Maybe it's forever, but it's only been around for a couple of weeks. So if you scroll up, scroll to the very top, Tom, and click on contracts, at the top bar. You'll be able to see the names. Flowverse has been very involved in getting their contracts upgraded. A lot of them are with Flowverse. That being said, There are approximately 800 and something active contracts right now in the ecosystem, or the most active contracts rather. So right now only 14 are on PreviewNet, really want to see that number enter the triple digits as soon as possible and preferably before the end of the month. That would be a good signal that a good like a decent portion of the community and ecosystem, is making effort to upgrade their contracts. But yeah, if anyone didn't know, Flowdiver now supports PreviewNet. So it's a very valuable source for those kind of insights. Nice.

11:49 - Tom Haile 
Thank you very much. You're welcome. Let me go back here. And so, For full CLI, here is... I knew that was going to happen. Let me bring that up in another... So for staging contracts, Here is the, I can see commands have been added to the PLO CLI for migrating. You can get more information using it, trying it out, and all that good stuff. Geo, do you have any words on staging and migrating contracts?

12:36 - Giovanni Sanchez 
Yeah sure, I mean like, I tested these out, I think Ian was originally working on this feature in CLI, and when I did initial testing, I felt like it was pretty straightforward, pretty easy. This, I mean, you would stage at the point that you have contracts that you've updated, to cadence 1.0 and obviously having done your tests this command in particular would allow you to commit that updated code into the staging contract where The cadence team will basically pull your updated contract and conduct the migration at the high coordinated upgrade So I recommend I mean you can you can go ahead and do this now as a part of this command There's also an unstaged contract. So if you just try it out on a particular contract and that you're working on, you can go ahead and stage the contract. I think it will actually also run a linter, like a Cadence 1.0 to give you like a kind of a final sanity check before it actually commits that code to the migration staging ground. But yeah, I would give it a shot and you can always, you know, it's a two-way door, you can unstage as well.

13:46 - Unidentified Speaker 
Nice, nice.

13:47 - Tom Haile 
And we'll get to Jordan later, talk about the different tools around just kind of verifying syntax and all that good stuff, all that yummy stuff. Thanks. Thanks, Joe. That's kind of

14:05 - Ali Serag 
And just to show you, I just shared in the chat, there's a more user-friendly guide on staging. What Tom's showing right now is more like the documentation reference for the five different commands that are added to the CLI. But if people want to go like, OK, I want to follow a guide where this is the first thing I do, I want to understand what staging is, and then this is the first step to stage my contract, et cetera, Ian also put together this guide called Migrate Smart Contracts to Cadence 1.0, which is under Cadence Slang Migration folder. And there's also a new migrating emulator state to Cadence 1.0 guide that's also been pushed.

14:56 - Tom Haile 
Thanks. I posted a link to it. I'll add that to the meeting agenda as well. Any other questions? BoHao, you got it? OK, you're good on that?

15:15 - BoHao Tang 
Yeah, I just got it off.

15:18 - Tom Haile 
OK, sweet, sweet, sweet. Then I was thinking we would continue on with the tooling around. The migration of contracts. Let's see, the linter VS code changes, and then we'll go to EVM tools, and then we'll go to dependency manager. Jordan, you have some words on that?

15:44 - Jordan Ribbink 
Yeah, I do. I think I kinda already gave a demo of the linter last working group session. I mean, a little bit's changed on it, but the general idea is the same. It's just like any other language. We've got a linter for cadence. It hasn't really been surfaced outside of VS code prior to this. It's being added into the CLI so you can do your static analysis check on your code. You can give it whatever files you want to lint and it'll it'll check both it'll do two things one it'll check that the code is syntactically and semantically valid and then on top of that it will also apply any linters that we have for any additional diagnostics on the code. Some of these might be warnings, some might be suggestions for cadence 1.0 changes. So if you've got certain semantic errors in your code that can be explained by changes to the language, it will give a better description of what you actually need to do rather than just saying this member doesn't exist or whatever the case. Yeah, I don't know if there's value in giving any sort of demo. Like I said, we already kind of did it. The good news is this is done now. It's just going through review. And it will be available in the cadence 1.0 CLI. So you'll go flow-c1, cadence lint, and then the files you want to lint. So I don't know, I'll just send it to the chat. Is your documentation I don't know where this lives exactly. It hasn't been ported back to the pre-Cadence 1.0 CLI yet, but that can be done after. Okay, cool, cool, cool.

17:51 - Tom Haile 
Yeah, yeah, yeah, that'll be good, that'll be good. Yeah, and then the VS Code changes.

17:57 - Jordan Ribbink 
To be honest, the feature's not fully done, but I can kind of give a bit of a demo-ish thing just to show what I'm talking about. Yeah, let's go. Yeah. I've got some bugs that I'm just working through right now, but that's always how it goes. Bugs are features. Yeah, exactly. Give me two seconds. Just got to share my screen. Yeah, I mean, pretty simple. But the idea is just giving more first class support in VS code to supporting multiple CLI versions on your system. So, you know, like how you have in other languages, you can change your Python interpreter or whatnot, you can change your flow CLI version, and it'll discover these binaries that exist on your system, since we now have a deterministic path, I guess, that the Cadence 1.0 binary exists in. And you can switch between them. This is also going to have the opportunity to install the Cadence 1.0 binary through here. And this just gives signaling to VS Code to use other Cadence 1.0 features, whatever those might be. One of those is that the testing in Cadence slightly 1.0 different because of the parser and whatnot. So it's important to have recognition in VS Code that you are using a Cadence 1.0 binary, you can switch to it, and you can switch back and forth. And so this will also configure your VS Code settings, wherever those are. But yeah, in VS Code, you have your .vscode folder, So as well, this will be portable between you and your other team members. So if you've got a repository that's configured to be on cadence 1.0 mode, it will be recognized and you won't have a bunch of errors that show up. There shouldn't be any additional configuration as long as you're committing your VS Code preferences. And yeah, short and sweet. Like I said, adding the ability to install the Cadence 1.0 CLI, update the Cadence 1.0 CLI, etc. Through VS Code.

20:30 - Tom Haile 
Can uh, can devs use brew to install the games 1.0 version of flow CLI yet? No, you can't use brew because the thing is brew doesn't support like tagged versions or anything.

20:42 - Jordan Ribbink 
Um So pre-releases can't really be shipped through brew So we are kind of relegated to the installation path of using that shell script. And so just wrapping up some of that functionality, like we already have in the VS Code extension, it offers updates for your current CLI and says, you know, there's an update available, click this button to update. And it does that through brew, but for Cadence 1.0, it'll just do it through the shell script. Do you have any documentation on that?

21:17 - Tom Haile 
Just to point users to it?

21:20 - Jordan Ribbink 
Yeah, that's kind of next step. Like I said, I'm not totally done the feature yet. And previously, I guess for context here, to configure Cadence had 1.0, to go into the preferences manually and set the flow command. To wherever your cadence 1.0 binary is, et cetera. And it just, it wasn't the simplest process. So this is just trying to reduce some of that friction when developing your cadence 1.0 contracts in VS Code.

21:52 - Tom Haile 
What about outside of VS Code, just to, you know, spin up the emulator and all that kind of stuff?

21:58 - Jordan Ribbink 
Yeah, so that's done through the Cadence 1.0 flow-c1. And so you can install that using the installation script for that CLI that we have in our documentation or in the Cadence Lang documentation, as well as on that forum post for the Cadence 1.0 upgrade guide. Um, this is something that was recently added. I don't know if we've covered it in this session at all. Um, but that is not prescribed path for installing your cadence 1.0 CLI as opposed to either overwrite overwriting your existing CLI installation, um, or having to download this binary manually and point to it and messy stuff. I gotcha. I gotcha.

22:48 - Tom Haile 
Yeah, I'll find it and I'll, I'll link it in the, in the agenda. Okay, cool, cool, cool. Yeah, so that would really help, I guess, smart contract devs in order to pull down the tools needed in order to kind of test locally their stuff. I know we put out some videos, you know, put out a video which would help and, you know, we keep moving forward to make it easier and easier and stuff. I'll make sure and link to that documentation on cadence link.

23:15 - Jordan Ribbink 
Yeah and on that note somewhere that you know this this stuff can maybe be documented or updated um is we have that short little video that geo had me made um for how to use the cadence 1.0 emulator and

23:30 - Brian Pistone (BoiseITGuru) 
this was made before the time of this installation script So things were maybe a little bit different then. But now you can use the installation script, and then when you want to go and switch onto VS Code, onto your new, or sorry, onto your Cadence 1.0 project, you can just click this button instead of having to do any sort of messier configuration in that regard. All right, bye. I was just gonna say you mentioned a like a config file So if you once you update it, you know using the flow 1.0 CLI DS code. Is that just in a Hidden folder in the directory or something. I was just curious because I started working on uh, I don't know if you guys have ever used Like use Use node or node package or node version manager, but I basically started working on a and code for a used flow version, which until the CLI had its own dedicated path, it was a pain to switch back and forth between them. So this automatically detects a config file in your directory and then creates an alias within your path for what do you want the flow for flow CLI to point to. And automatically updates that way. So I was just curious, because if it's using a config path in a folder, I wanted to try and update my tool to that, because then regardless of what, you know, what project you're working on, you can just jump into your folder and your terminal and everything's just pulling the correct flow CLI version.

25:12 - Jordan Ribbink 
Yeah, so we don't have any sort of like formal version manager, like node version manager, the way that we're kind of working around. I know I built it is what I'm saying.

25:22 - Brian Pistone (BoiseITGuru) 
Okay, gotcha.

25:23 - Jordan Ribbink 
Yeah.

25:24 - Brian Pistone (BoiseITGuru) 
So the way we've done it is we've aliased.

25:28 - Jordan Ribbink 
We've aliased flow-c1 instead of flow for the binary name, just because I guess maybe it's a little bit easier for something that's a bit of a one-off thing. Like Node version manager, you're managing consistently a bunch of different Node versions, whereas this is kind of a one-time, one-and-done thing. Hopefully. Maybe a similar... You know back a very long time ago when python switched over from two to three they went and they changed their command to python three instead of python and so that's kind of maybe where the inspiration for this comes from and for some alternate reasons that. It's easier in tooling to, I guess, use this version configurably or by default or whatever, if it always exists at flow C1, instead of trying to interact with some version manager in order to control it. Like in VS Code, like I showed you, you'd have to be configuring the version manager somehow, and you'd have to be setting environment in your terminals, etc. It would just be a lot of overhead. It. Right. Well, I mean, I guess that's what I'm kind of asking.

26:45 - Brian Pistone (BoiseITGuru) 
How does the the when you when I go back into VS code, you mentioned there was like a config file or something that it knows this projects using the C one. And this one's not. Yeah, sorry.

26:58 - Jordan Ribbink 
Yeah, maybe I didn't play that the best. I just mean your VS Code preferences. Like, you know, when you edit your preferences for your workspace in VS Code, you have your .vscode folder, and then whatever preferences or settings, not JSON. And so we have a configuration variable. Cadence dot low command it already exists. You can go and you can look at it now But but just surfacing this through UI instead of having a user have to know manually that they have to edit this Yeah, it should help a little bit Okay, cool. That makes sense. Thank you Nice.

27:41 - Tom Haile 
Thank you, Jordan. And I nominate Jordan to do a new vid on video for the installation of the K820. I think that'll be awesome if you choose to accept it. And then the last thing in the tools for kind of the new Flow EVM section of the whole crescendo upgrade would be the hard hat remakes. We have tutorials on those. These are all standard EVM tooling, and there's been a request for a WAGME tutorial, so we'll create one of those. We currently have some PRs out to get the Flow EVM networks integrated with the larger EVM ecosystem. Therefore, it'll be a little bit easier for development using these standard tools, and that they'll have Chloe VM networks kind of baked into the configuration stuff. So there won't need to be kind of custom configuration for you the clients for accessing Chloe VM and in that regard why me would use VM which uses its own hopefully soon, hopefully the PRs will get merged up soon, and then it'll really make the tutorials simple for specifically the Wagny tutorials. And I'm just curious if anyone had any questions or requests on EVM tooling that we can add to the docs.

29:31 - Brian Pistone (BoiseITGuru) 
Not evm tooling, but can we get the go versioning? Situation sorted out every time you run a go mod tidy.

29:38 - Tom Haile 
It blows all the pragmas up everywhere Does chase have any uh Input on that one. I know ian would probably have some uh opinions on that but case you have anything uh We've been you're talking about which library specifically because yeah, we've been just trying to get all of the go packages with everything being

30:04 - Brian Pistone (BoiseITGuru) 
in the process of being kind of split out into the multiple repositories right now if one updates, you know is on m7 and one's on m8 then the pragmas get all or the protobufs and different pragmas get all blown up and And the program just won't even run anything that imports it and you have to manually go back and like go get your specific version every single time And because of the way the releases are being done if you don't specify your versioning It's automatically going to the cadence one version instead of the stable versions Which depending on what you're working on may not be what you want. Those are pre-release still, you know So it's just, it's literally slowing down work by weeks because every time I add a A cadence client or anything, I have to manually go in and verify which version of each individual on flow package I have across, you know, sometimes I'm working on, you know, four modules and then, you know, I got a manual update them across all four. So that one program will run.

31:06 - Unidentified Speaker 
Yeah.

31:07 - Chase Fleming 
Uh, huh. I feel your pain. That's the best thing I can say to you. I must have spent probably, I think me and Jordan here combined, we like have been dealing with dependency issues for probably like three weeks now. Hopefully it's in a better spot. Cause we were at the same spot where like, we're mostly working on CLI or something. Right. But like, so Flow Go changes, the Go SDK changes. And like now it has to make its way all the way up through like Flowkit and then all the way to CLI. And then there's also like the Stablecators branch and then the regular ones. And if something gets missed, then you got to cherry pick it and then rework it all the way up. So it's a little bit of a nightmare right now. I think we've solved a lot of the issues recently related to like the crypto package that was causing problems on certain branches. Yeah, so hopefully that's um, I think like we've got that into the master branch now not just the stable cadence one on cli So hopefully that should be kind of like worked its way up um and then Hopefully people are following somber properly. Um, I I don't know When we'll just be working off of like one master branch because we still have to ship stuff um on like cli in the meantime, so I don't have like a it's going to be a lot easier. But I do think it recently, it will get a lot easier with some of the crypto things and stuff that have been fixed. So I don't know, Jordan, do you want to chime in on that?

32:43 - Jordan Ribbink 
Yeah, I guess like, Um, from your description, maybe I just wasn't a hundred percent sure on the specific issue you're facing. Like, yeah. And in general, we've had a lot of, um, troubles with dependencies, but I don't know if our work has, has covered the issue you're facing Brian. So like, if you can write up some sort of issue or, or somewhere, I don't know where that needs to live. Um, and, and just tell us to have a look that maybe we could see if we can help at all with that. Um, Yeah, that would be most useful probably.

33:19 - Tom Haile 
One thing that might be interesting just to kind of put a book into is Flow Kit. So has Flow Kit been fully pulled out and has it been pulled out only for v2 or also for, you know, pre-Cadence 1.0 stuff?

33:34 - Chase Fleming 
That's its own library now and that one should have all the crypto stuff, I believe, fixed as well on both branches.

33:45 - Jordan Ribbink 
As of OCLI 1.13.1, believe, LoCit had been broken out into its own repository.

33:53 - Tom Haile 
That's what I thought. I just wanted to get the current status of that. That's awesome. And speaking of dependencies, why don't we just focus on smart contract dependencies? Chase, you want to give a blurb on the dependency manager? Oh, yep.

34:12 - Chase Fleming 
Actually, can you pull up this link right here? Or actually, you're not sharing. I can share it. That's fine. It's a lot easier. Is that OK? Go ahead. Um, so yeah quick quick summary on dependency manager. This is a feature that came out Honestly, when did it come out maybe january or something, but we haven't really talked about it much yet. Um, we've been pretty um busy with the cadence 1.0 and ebm stuff but worth at least mentioning now, um, this one is not related to those this is just a tool and hopefully a larger feature to Make your lives a lot easier So the problem that it's trying to address is the sort of copy paste smart contract dependency problem, right? So if you want to go build something on top of float, right, and you wanted to develop locally with it, you'd need to actually, you can probably pull up contract browser. And see float. And so we want to come in here, right. And our first step would be like, okay, I'm going to copy paste this whole contract. And then in order to get it working locally, I also need to copy paste everything else that it depends on. Um, So those would be things like the a lot of these are core contracts, right? So But there are other pieces as well. I believe like is fine to views. I think that's that's not so you'd have to pull these in copy paste it as well into your Local project and then you'd have to go into your flow json and then you'd have to add every single one of these contracts you'd have to put in their aliases and then you'd want to keep them up to date, right? Oh, and then you also need to add them to your deployments, right? So there's a bit of like tedious manual work there. So the problem that this is aiming to solve is sort of like a npm install or, right? So I would be able to go into my flow CLI. And I would say, hey, I want to flow dependencies add, I would say the network. So I want to pull float from this address on testnet. And this will be my source of truth. And, um, it's going to go through and it's going to add in that contract. It's going to pull in here, uh, this whole contract, and then it's going to look at every single one of its imports. And then recursively check all of its imports until it pulls in everything you need locally. And if you, if you already had it locally and you ran it again, if it saw one that was newer on the network that had maybe been upgraded, it would ask you if you wanted to upgrade it. So that's going to pull it all in. And then it's going to also automatically fill it in. To your flow JSON. And then, so it would look something like this. If it is a core contract, it's going to automatically fill in all of those aliases for you. So emulator, testnet, mainnet, and we'll have to add previnet support as well for this. And so then that gets added to a dependencies thing. So then you'll be sort of separate in your flow JSON where you'll have your contract section. For the things that you're developing locally. And then you'll have this other section, dependencies, that you probably shouldn't touch at all because they're things that you depend on. And so basically, yeah, trying to simplify your life. And those will get all added to a local imports folder that you can get ignore, kind of like node modules. And yeah, and that's the current state. I'm currently working on another ticket too, where it's going to ask you if you want to add it to deployments and then let you select between which accounts you want to add it to. So then that would also solve the, hey, I now need to deploy, let's say, float and find views, but not non-fungible token, all that. So it will try to solve all of that setup for you and hopefully save you a lot of time. So any questions on that? I assume it works in Emulator for local development? So you would pull in, you'd pick your source of truth, like, you know, that's kind of what it's solving, right? So you say, I want to build on float locally, I'm going to, I can pick do I want to work off the testnet or mainnet contract, I'm just going to pull it in, then it would, and you can add it to deployments, and then you could deploy it with like flow project deploy. And so then you'd be working on your local version of float. But you didn't have to do any copying and pasting and adding it to deployments and all that. Right. That's awesome.

39:11 - Brian Pistone (BoiseITGuru) 
Will it automatically add non core contracts to the deployments for emulator? Or do you have to manually still do that?

39:19 - Chase Fleming 
Uh, that is the adding them to deployments. That's the next ticket I'm working on. I have a issue for it right now. So right now you would manually add them. Uh, you'd, you'd go put float and find views, but literally the next thing I'm working on is, uh, And I'm trying to do it in uh, there was a couple different options where I could be like Maybe gonna add a flag and then you just say what account you want to but it would be much cooler if it could Let you just it would detect all the accounts you have and then let you go through a selection and

39:51 - Brian Pistone (BoiseITGuru) 
say I love it. Yeah. Okay, cool.

39:58 - Chase Fleming 
You like that approach? So that's, yeah, that's what I'm thinking. And hopefully that'll be done soon. That's the next feature to get added onto this is the deployments. Anything with less flags.

40:08 - Brian Pistone (BoiseITGuru) 
I feel like I lose my mind sometime trying to remember all the flags that I have to use.

40:13 - Chase Fleming 
Yeah, I agree. No flags, interactive, make it really nice and clean.

40:21 - Tom Haile 
I would also suggest having a non-interactive mode. So it would just help devs that have massive contract suites just to run through a configuration, like a shell script or something like that. Totally agree.

40:36 - Chase Fleming 
There will be a flag probably for skipping the interactive mode, right? So that's simpler. So it'd be like if you, because then if you're in, I don't know, maybe you have it in some sort of like shell script you're running or something where you can't do the interactive And you're just like, hey, just install everything for me. That would be where I'd be like, skip interactive or skip dependencies or deployments. Nice.

41:02 - Unidentified Speaker 
I think that's awesome.

41:04 - Chase Fleming 
Check it out. If you see any other features you want added on there, I think, yeah. The next thing, like I said, is deployments. Maybe a thing for also adding aliases at the same time if you need it. And if you think of anything else you want in this, let me know.

41:24 - Unidentified Speaker 
Awesome.

41:24 - Tom Haile 
Thank you very much, Jace. That's going to be awesome when we get all the migration upgrade and all that stuff done. And I think the last thing we have on the agenda, Ali added, any discussion on tools that are missing to help out in either EVM development or contract migration or even on the other side of the crescendo upgrade. Anyone have any, anything they want to talk about? Of course, I'm shilling flicks. We'll have more flicks. Functionality, you know, when we get back to that as a priority. I know Brian's doing a lot of work updating FlixKit in order to better integrate with his service that he's adding. And so it sounds like after contract development, you know, maybe FlixGeneration would be the next step in order to create the artifacts for integration of third parties who can easily use your contract suite. How do you feel?

42:40 - Brian Pistone (BoiseITGuru) 
That's one thing I've been going back and forth on myself. Do we want to make the, and I mean, maybe we want to do both. Do we want to have it so the SDKs can just very cleanly interact with Flix? Or do we want to actually create tooling so people can build SDKs in certain languages to interact with their contracts? Hmm.

43:05 - Tom Haile 
Yeah, there is an aspect of code generation with the Flix stuff. But of course, you need to generate the Flix in order to build that base layer in order to vertically grow, right? So we have JavaScript and TypeScript and potential tasks down the road, the Golang code generation. But I mean, there's no So no stopping someone from just generating their own language, because it just leverages templates, you know, building templates. But you did bring up a good point, and I would say topic for another conversation, since we're kind of focusing on the Crescendo update in this particular meeting. But I like where your head's at, though. All right, Mohal has a question. Where can I find a list of available commands for Flix? That is in the Flow CLI. I will grab the URL for you. And so here it's in the Flow CLI tools in the developer docs. You can just see there's three that are available currently right now. And then I think it brings up a very good point. Also, it would be really nice to have all the flow CLI commands in one place so you can look at them. How's that coming, Tom?

44:43 - Unidentified Speaker 
It's already there.

44:44 - Tom Haile 
Chase brought up a good point, and I'm kind of reorganizing that. So the all-help command, trying to get that PR pushed through, and I think probably based on conversation with Chase, the better approach would be to generate the all help inside the flow CLI along. So it would sit next to all the other, uh, you know, read these and mark down and then have the dev docs just linked to that. So that we don't have to worry about, you know, stuff being moved around, um, in the, in the developer docs. Oh, so yeah. Okay. Okay. That's a good one. Well, how, where are the actual templates? And so the, there's, uh, there's a lot of templates that have already been generated that, uh, live in a, in a service. I can, I can get that, get that for you right here.

45:51 - Brian Pistone (BoiseITGuru) 
Directed template service.

45:57 - Tom Haile 
So. Here are a bunch of templates. Now, these haven't been upgraded to the Kings 1.0 stuff, so these are on the existing networks testnet. I think some of them also can be applied to mainnet, but that's that. So all of these will need to be upgraded to Kings 1.0 once we get all the tooling. I mean, that's a decent thing.

46:24 - Brian Pistone (BoiseITGuru) 
Different conversation for a different thing, but just for food for thought, Tom, maybe in the CLI having, you know, cause the API service allows you to query it, but maybe more of like a find the method that reads all, you know, something to help you discover more of an interactive way of working with it.

46:42 - Tom Haile 
Yeah, there's, uh, there were changes to it to give a a simple search ability to search templates by title and description and messages. So there's a PR that's been in for a while. The idea is that there'll be other services that use the on-chain stuff, hint, hint, Mr. Brian, and that we would want to shift to that kind of service that relies on the on-chain representation of the flex opposed to everything kind of an off-chain thing that things could change and stuff. I think that'll be great for allowing third parties to integrate easily. I like your questions, Mr. BoHao. And we are in this Cadence Upgrade, so we're kind of in a little bit of a flux with Flix. But we'll get on the other side of the Cadence Upgrade, and then it's full steam ahead on Flix. I think that's it. We have a few more minutes if anyone has any questions or any particular topics they want to address dealing with the game's upgrade and tools.

48:13 - Unidentified Speaker 
Okay.

48:14 - Brian Pistone (BoiseITGuru) 
Does any more work been done on that GBT, you know, the custom GPT that was being made for stuff? I just hadn't been in the meeting for a while, so I wasn't sure.

48:26 - Tom Haile 
Yeah, Ali, do you have any, any insight into that? I know Naveed spent a lot of time and it is available. Of course you need a chat to get access to it.

48:44 - Ali Serag 
Let me share the link right here.

48:47 - Tom Haile 
Do we have that link available in the dev docs or is it kind of an aside?

48:53 - Ali Serag 
It should be in the dev docs. Yeah, if you go to the migration guide, like when I'm trying to position the migration guide, it's like the single source of truth for like all the links for the relevant documentation, educational material and tools that as well as in person support you need. So if you go to the migration guide, and you scroll down to helper tools, you'll find the custom GPT there. But again, we can't fully rely on it, because I want to add that disclaimer. I don't want people to copy-paste their code into it and then have this false sense of security that, oh, it's going to work perfectly. People will still... I mean, hallucinations happen all the time with these AI tools. You're still going to need to... From developers I've talked to, including devs on the Dapr Labs team, they said it's been very, very helpful already with facilitating their migration, but you can't 100% rely on it. You still have to manually check it and make sure it makes sense what it's spitting up.

49:58 - Brian Pistone (BoiseITGuru) 
Well, I mean, that makes sense of all AI and coding, right? Sometimes what it gives me is very interesting. No, I was just thinking that would be a cool video to make to help kind of show people that not just in terms of like, Hey, here's this tool that can help you migrate your code, but even something that you could, you know, because it's a chat bot, you know, get giving some sort of video that shows the decrease in opportunity costs and developer costs to help you get started as opposed to here's just all the documentation.

50:38 - Ali Serag 
I love it. If you if you want to volunteer to make that video I'll put it on the migration guys Where's jacob when we need him Exactly. Uh, well jacob's working on a lot of um important stuff right now right now.

50:53 - Brian Pistone (BoiseITGuru) 
He's working on a video to show end-to-end staging process um yeah, I mean if I have time I I love making videos like that, but machine. That can be another whole nother working group as we each other be great.

51:12 - Tom Haile 
Well, you can you can build a LLM of yourself and then send it out as an autonomous bot. It's coming. Oh, nice. Good call out on the on the duty. Anybody else have anything they want to discuss? We have a few more minutes. If not, then I think that's all we got. I'll hang around for a little bit. We do have the community developers meeting here in a couple of minutes. You want to jump in the Discord. If you have any questions on migrating contracts or Kings 1.0, then come on over. We'll be hanging out, be available. Okay. Thanks everybody. Appreciate it. Thank you.

53:26 - Ali Serag 
Silence.
