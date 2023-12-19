---

layout: single
title:  "Applied Reinforcement Learning Reflections "
---
# Overview
*Here I reflect on work on implementing autonomous systems in large manufacturing companies, and I draw some insights for future autonomous agents work.*


# Autonomous Agents
I spent two fascinating years with the **Autonomous Systems** team at Microsoft implementing Reinforcement Learning solutions on industrial problems. This team had a vision to make autonomous industrial systems a reality. We were building a platform and an ecosystem around the idea that some control problems in industry are really hard for a human to do, but much more tractable for an AI. I think this team was ahead of its time, and that in the coming years the idea of self-learning algorithms driving optimization and making autonomous decisions in an industrial context will become much more prevalent.

I think that before we have autonomous agents acting in industrial settings, we'll probably see them come up in other areas. For instance, [Auto-GPT](https://github.com/Significant-Gravitas/Auto-GPT), [GPT-Engineer](https://github.com/AntonOsika/gpt-engineer), and [baby-AGI](https://github.com/yoheinakajima/babyagi). Entire companies have sprung up around this kind of technology, promising that it will be able to do market research for you or build entire websites or software tools. Give these agents a high level task, and let them make a series of decisions independently. Personally, I am skeptical that with the current tech these agents will become anything more than a prototype. And it seems like others are coming to similar conclusions. Embra [pivoted away from agents](https://twitter.com/zachtratar/status/1694024240880861571?s=20) and also see [this thread](https://twitter.com/sjwhitmore/status/1645811222661718021?s=20). Still, I think as the core AI technology develops, the AI will be robust enough to chain together more and more actions until it becomes very much like an autonomous agent. 

![Embra tweet](/assets/images/Twitter_embra.png)

Now the tech we were working with was very different. We were working with simulations, numerical (rather than text-based) problems, industrial contexts, and we were using RL to solve these kind of problems rather than LLMs. Still, some parallels can be drawn. What does it take for a human to give up some decisions making control to an AI? What did I learn deploying these systems on real problems, and what lessons can be taken to this next wave of AI agents?

Below is an assortment of my reflections. Some of it will be applicable to any new project implementation at a large org, and some of it will be more relevant to implementing autonomous agents specifically. 

## Select an impactful problem
You need something that is important enough for your project to get traction and for people to put resources up. If you were to create an AI agent that replaces X task, would that be a big deal? How big a deal? You need to find a way to estimate this, and you need to frame it in the right way. The decision makers and funders of the initiative need to be immediately convinced that if your system works, it would be important. The way they think is in increase in revenue, increase in time to market, reduction in cost, improvement in margin, etc. Learn to communicate in their language. 

**Make sure the problem is the right application of the tech**
Your technology is not going to be able to do everything. For people not steeped in the world of AI, these systems will be very new. And I think that many engineers and builders of this technology underestimate how hard it is to select the right problems. The sales team will make contact with a new group who might have heard some new things about your technology, and together they will try to figure out what the scope of the implementation of your technology should be. This is a very difficult problem. Understanding a company's processes and problems by itself is hard. Then in addition you need to know whether your solution will actually solve those problem. Try to make the problem of finding the right problem as easy as possible. You should try to write down a decision tree of what attributes for a bad, average, good, and great application of your technology. Work with your sales team to create this decision tree, and see if the thing you are building actually aligns with what the customers you're talking to want.

## Understand the objective
What are you optimizing for?** People are bad at articulating what they actually want. *"I want to improve efficiency while maintaining quality?"* Ok, but what does that actually mean? Your goal should be to try and get to a sufficient understanding so that you can math this. Can you write down the objective function as an actual mathematical equation where you can plug in the variables and calculate the current performance?

One helpful tip, once you've gotten this function you should try to test it out with the various stakeholders. Try providing some conflicting examples that by the definition of the function should be equivalent, but you suspect aren't. This tends to be a great way to get more conversation going. "Oh, no you're actually not suppose to ramp up this variable so quickly" or "you cannot have this variable higher than that variable. Thats a safety risk."

Simply asking customers what they want is never going to cut it, but putting some examples in front of them tends to bring out a lot of additional constraints. 

**Identify a reasonable baseline**
What is your north-star? An increase in total widgets produced? A reduction in re-work? An improvement in total sales? An increase in total throughput? What is the current level this is at? And how is this currently done? If its an important enough problem, then they will have tried to solve it in the past. What went wrong? What can you learn from that?

You should try to have a conversation about how you will test this. What is a fair test to compare your technology against the current baseline? At some point you will come into the counterfactual problem. *"yeah you got good results, but can you show that it was better than if we didn't make this decision? What if this was just a particularly easy batch?"*. That can be a hard problem to solve. In some cases you can throw statistics at the problem, but if there aren't enough samples in the data (e.g. you only do X task once per week, and you need >100 samples to demonstrate with sufficient statistical power that its indeed better), then statistics won't cut it.

Head to head tests (get a human and an AI to solve the exact same problem) can be helpful. But this is also not always feasible. 

Are you running the comparison in the real world? Or in a simulation? The benefit of running in the real world is that you have more guarantees that its realistic. But the results are often slower, with less control over noise, with higher stakes.

You should come to an agreement on the benchmark and the goal of what constitutes "beating the benchmark" before you conduct the tests. People always want to get more and better performance, and they will shift the goalposts.

## Define the states and actions
Take an example problem end-to-end, taking note of the states (what information should be available to the agent at each stage) and actions (what decisions can the agent take?).

Are all of these states and actions actually available to the agent? Often the information and decisions might be stored or take place in multiple systems. Humans might be able to access all these things, but can your bot? Does your AI have API access to each of these systems? If not, there might be a lot of implementation work to be done to even start your prototype. Don't underestimate this work. Surprisingly often we ran into problems where getting one system to connect to another system was a few weeks of work.

## You need to instill trust in the AI
Think of this as a journey with stage-gates you need to bring them on. You might believe in your vision, but others will not at first. Don't think you can show some statistics in a slide deck and expect them to be immediately swayed.  First you need to get them interested enough to commit resources for a prototype / trial, then you need to convince them to deploy the prototype/trial, then you need to convince them that the prototype/trial was successful and that they should deploy this in production. The bar for each of these stages is different and the kind of data the stakeholders expect will be different.

## People want to feel like they are in control 
The way I've seen this show up is two fold. (1) people want explainability, and (2) people want these systems to call for help if they are out of their depths.

Really I found that this is part of the "instilling trust" point. Stakeholders want evidence that they can trust these systems. Why did X happen? Why not do Y? Is the system making these decisions for the right reasons, or did it stumble across a reasonable looking strategy for the wrong reasons.

Sensitivity analysis was often helpful and understandable for the explainability side of things (if I change these inputs, then the AI behaves differently in this way).

## Find the right people you need to convince
Regardless of how great your technology is, at some point you will need to convince some people of its efficacy. Do not underestimate the importance of human connections. The big stakeholders here are; 

1. **The people currently doing this job**. You might think there is a strange dynamic here in "training your replacement". The way I always thought about it is that it makes sense to up-level yourself. Automation is coming, and its better to ride this wave then to be crushed by it. In my experience, without someone who has intricate knowledge of what the job to be automated actually entails, your system will fall flat. There are intricacies involved in any task. These aren't necessarily unsurmountable, but these details are painful to learn by running straight into them. Instead you want to work with people on the ground floor from the beginning.

All that being said, I have yet to come across a system that fully replaces a role. Instead, it makes people doing the role currently more efficient (and therefore might reduce the total headcount of people doing that role), but it doesn't outright replace the entire function. So this makes this person doubly important; they actually have to work with and/or operate these autonomous systems. If they don't find these systems useful, then they won't use them, and therefore your autonomous solution won't have any impact.

2. **The people with decision making power**. There tends to be many people in an organization that can block your proposals on some grounds that they have responsibility over. In the manufacturing circles you'd want to make sure you're engaged with the operations, safety, finance, IT, during the design stage. Often there are multiple stakeholders in each of these groups, but every organization is different. No one wants to feel like they were side-stepped. If you can engage these people early and hear out their problems and take steps towards addressing them, they can become allies. 

3. **The Champion**
You need someone on the inside who believes in your vision and who can clear blockers for you. This person tends to be a few rungs higher up in the corporate hierarchy than your immediate working/implementation team. They can tell you about initiatives you can align yourself with, concerns that specific stakeholders raised that they aren't publicly voicing, provide context on who are the key decision makers, and much more.

In my experience these are the people who are staking their career on your vision. They will stick their neck out for you. In return, you should be candid and transparent with them about the opportunities and the risks.

# Takeaways
- Don't underestimate that you need to convince real people to implement your system. There is a fascinating paradox here; we are trying to build these systems that make decisions independently of humans, but at the same time their success is deeply tied to human acceptance and trust. Bring people along this journey early, and prioritize it throughout the process of implementing an autonomous agent. 
- There might be significant plumbing that needs to happen to ensure that the AI system has access to the same information as the humans currently doing the tasks. Current processes are built for humans to access. Connecting your AI with all of these systems might not be as trivial as you might expect. There is a lot of hidden knowledge that is implicit in human decision making.
- Put in a lot of effort in making sure you are optimizing for the right things. In my experience getting RL agents to do what you want is a very difficult job. It seems like the AI continuously attempts to deliberate misinterpret your intention. This is the classic alignment problem - writing down a fool-proof objective function is very hard. 