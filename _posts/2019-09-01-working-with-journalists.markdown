---
layout: post
title: "Working with journalists makes me a better engineer"
date: 2019-03-04
tags: process, working
---
<!-- markdownlint-disable MD033 -->
<!-- markdownlint-disable MD026 -->
<!-- markdownlint-disable MD002 -->

_Note: If you aren’t very familiar with my place of work, BuzzFeed, you may not know that our newsroom, BuzzFeed News, produces fantastic journalism. This isn’t a post about proving that point, so if you are thinking “Heh, BuzzFeed? News?” please first [check us out](https://www.buzzfeednews.com/article/maggieschultz/buzzfeed-news-biggest-stories-of-2018) 💖. Ok, read on._

I've worked at BuzzFeed as an SRE for over a year and a half. In that time, I've also worked with our [Tech + News Working Group (TNWG)](https://tech.buzzfeed.com/tech-and-news-working-group-7dabaaa38e45) with BuzzFeed News. At BuzzFeed Tech, we have "7% time" to spend on any learning activity we choose, and I spend that time working with our newsroom.

We created the TNWG to pursue a mission:

> Our mission is to act as an elevating force for the newsroom’s work through guidance and assistance using our technical skills. Our News team at BuzzFeed strives to shine light on the most important issues facing us. Currently, this means a growing focus on the impact of the internet and technology on a range of topics covered by News. As a team of technical experts, we are uniquely equipped to assist in this realm.

Over the last year, we've consulted with journalists on a variety of stories, and even built tools that made a few of those stories possible. In one instance, we built a bot that watches YouTube based on a set of search terms and returns a report on all the data with all the data from its trip [down the recommendations rabbit hole](https://www.buzzfeednews.com/article/carolineodonovan/down-youtubes-recommendation-rabbithole).

While our mission and work concentrates on what the tech org can offer the newsroom at BuzzFeed, this post is about the ways the newsroom has helped make me a better engineer. I have had the privilege of observing our reporters at work and many of those lessons carry over to my job as an SRE.

## Communication communication communication

When it comes to explaining complicated topics succinctly and clearly, no one has a harder and higher risk job than journalists. Often it takes our reporters just minutes to notice a breaking story and write a polished 200-word take. In these moments, they’re deploying years of hard won experience and skills. Furthermore, what’s impressive about these communication skills is that they’re balancing responsibilities among multiple reporting desks (breaking news, tech, politics, etc.) while also ensuring they meet a rigorous level of journalistic standards and ethics. The risks are far more acute than those we face on the engineering side, where colossal disasters do not generally ruin careers.

As an SRE, I'm often in a similar situation, except we face time-sensitive issues across products. If an incident happens, we have to notify a host of interested parties and we have to do it in a consistent and responsive way. When facing an incident, journalists have taught me to:

* Clear out extraneous noise
* Quickly identify the point people necessary to solve our problem, and
* Practice our communication skills and communication plans in advance

Skills gleaned from my pals in news have helped make me and my team get better at communicating calmly, clearly, and efficiently. We work to maintain a shared language as a team, and an understanding of what we'll do if something unexpected happens.

## Research is a long game

The best journalists are world-class researchers, and furthermore, expert open-source intelligence (OSINT) analysts. I've picked up lots of tips and tricks from talking to reporters about how they search for information online. When it comes to OSINT, engineers have tips and tricks of our own. Sharing these insights with one another has brought TNWG members great joy whether it’s explaining to reporters how they can run an OSINT software on their own through Docker or a journalist flagging a vulnerability in our system that they saw through their research.

The main lesson I've learned from the newsroom is that research is a long game. Not every story is going to work out, and many of the leads I've seen our journalists pursue have turned out to be dead ends. Thankfully, our news team tends to be quite good at recognizing a dead end and avoiding the [sunk cost fallacy](https://www.behavioraleconomics.com/resources/mini-encyclopedia-of-be/sunk-cost-fallacy/).

In my experience, we on the tech side of the TNWG seem to have a harder time halting effort in the face of unlikely returns. A reporter will come to us with a question and we'll run with it. We'll answer the question, get invested, and keep pursuing the angle. Soon after, the reporter will realize we’re at a dead end and move on to another question or story, but there are often engineers still doggedly looking at the question days later. I've learned from journalists that when a trail runs cold, it’s better to turn around than drive down the road of diminishing marginal returns. Document what you've learned and where the trail went cold, and move on.

We struggle with this immensely in our software projects. You get really invested in a piece of technology or a certain solution that it feels like there is no way to move forward unless you are on that path. This is not true. There's always another solution, another technology, and learning how to admit the trail's run cold is an immensely valuable skill.

## Just talk to people

Possibly the hardest thing to imagine myself doing when I watch reporters work is that actually talking to people, like, on the phone. Reporters are constantly talking to contacts within governments and companies, keeping in touch with sources, or chatting with other reporters through text, in person, on the phone, etc. All the time. When digging into an issue with a reporter, the first time they said, "Well, why don't we just ask them if this is what's happening" I thought, "Wait, you can do that?"

Working with journalists has helped me come out of my shell a little bit in terms of my willingness to talk to people. It has also impressed upon me the importance of maintaining good relationships with everyone I meet in the tech community. I try to be kind to everyone regardless, but I think this impressed upon me the value of networking, especially in open source communities. While reporters are often seen as antagonistic or single-minded, good reporters know how carefully they have to treat relationships with their contacts and potential sources. Similarly, in the software world someone is far more likely to help you fix a bug or solve an issue if they know you.

## Striving for truth isn't finding answers, it's asking questions

This is by far the most important thing I've learned. When looking into any given lead or scoop or topic, it begins with asking questions and more questions and more questions. Often the best reporting is just putting questions out there – why is this technology monetized this way, who funds this campaign, why was person X here at this time, why is the court system set up this way in the first place? I've seen reporters ask questions that I would never think to ask. These questions don't always uncover surprises or elicit confessions, but sometimes they uncover something where no one thought to look.

As a developer, a reorientation towards questioning is crucial. It often uncovers more bugs than a straightforward read of a pull request, for example. It leads to more creative solutions for tough problems. It pulls me out of biases towards certain technologies. It makes it easier for everyone in the room to understand what's going on. Focusing on the questions and coming up with the most creative questions makes your team more imaginative.

## Finally, working with journalists gives you Range

I recently read David Epstein's book Range: Why Generalists Triumph in a Specialized World. In the book Epstein argues that by generalizing and studying many different ways of working, we set ourselves up for success in our specialty. From the book:

> Modern work demands knowledge transfer: the ability to apply knowledge to new situations and different domains. Our most fundamental thought processes have changed to accommodate increasing complexity and the need to derive new patterns rather than rely only on familiar ones. Our conceptual classification schemes provide a scaffolding for connecting knowledge, making it accessible and flexible.

This is why I love working as an engineer on a platform that supports non-engineers. I get to talk and work with people who do things very differently from me every day. There is so much we can learn and apply from fields apart from our own and I think that's been especially true of my time working with our newsroom. I get paid to write code, but coding itself is such a small part of my job. On the other hand, the ability to communicate what's happening in my code, the ability to research how to express something I've never done before in code, the ability to reach out to people who also write code, and the ability to ask good questions about code? These are all invaluable skills that make my work better. These are all skills I am still learning, and I'm grateful that I get to learn them from the best of the best: Journalists.
