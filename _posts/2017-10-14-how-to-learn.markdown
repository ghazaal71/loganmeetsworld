---
layout: post
title: "How to Learn"
date: 2017-10-14
tags: learning
---

For the past several years, I've been thinking a lot about learning science, or the systematic investigation of how we learn. This was fueled by a switch in career trajectories after I graduated college towards software engineering.

There's this really intimidating article that I often hesitantly send people looking to get into site reliability or ops work. It's [A roadmap to becoming a web developer in 2017](https://medium.freecodecamp.org/a-roadmap-to-becoming-a-web-developer-in-2017-b6ac3dddd0cf) and lays out a list of topics that one can attempt to learn in various fields of web development when they're trying to break into a field. Here is the graph of things to know for the "devops" path:

![devops topics graph](https://cdn-images-1.medium.com/max/2000/1*Qc0PqmXenUZmRvnkMh9AoQ.png)

Wow, this is making me sweat just looking at it. Needless to say, there's a lot to learn.

In May, I gave a lightning talk at Monitorama on learning and it's connections to my job as an ops engineer: "Optimizing for Learning". You can watch the talk [here](https://vimeo.com/221064922) at 6m7s. The talk is an exploration of why memorization and learning are important whenever faced with a seeming abyss of knowledge.

Software engineering is an incredibly broad field. There are a lot of topics to just _know_ about, before you can even get to mastering them. This is particularly true for systems and ops engineering. Entering this field really overwhelming. In the talk I have identified one source of this overwhelming feeling - Ops is based heavily on expert intuition and experience. Experience takes time, which we often cannot control. However, I decided in the last year to balance this disadvantage with something I have slightly more control over: My learning and memory. I decided to give that talk and write this post because I realized this is a challenge everyone faces. The faster you can learn new things and connect them to what you already know and the problems you’re facing, the more effective you are at your job or starting to build something useful.

Now, learning is incredibly subjective and brains are complicated. No one learns quite the same. However, I have found some patterns that have made me better at it, and I'd love to share them.

## Hierarchies of Learning

I start theoretically with some conceptuals diagram that I learned all the way back in the 9th grade, [Gagne's hierarchy of learning](https://www2.rgu.ac.uk/celt/pgcerttlt/how/how4a.htm) and [Bloom's taxonomy of learning](https://en.wikipedia.org/wiki/Bloom%27s_taxonomy). There have been many adaptations and addendums to these hierarchies since Robert Gagne and Benjamin Bloom came up with them in the 1950s, but I find the general path of learning to be an effective mental constructs for me.

The idea is that learning increases in complexity up a hierarchy and learning can often be more successful when focusing on the lower rungs, listed here lowest to highest. Here's Gagne's hierarchy:

1. Signal learning
1. Stimulus-response learning
1. Chaining
1. Verbal association
1. Discrimination learning
1. Concept learning
1. Rule learning
1. Problem solving

And Bloom's:

1. Remembering
1. Comprehending
1. Applying
1. Analyzing
1. Synthesizing
1. Evaluating

You can see we start at the lower levels with stuff like route memorization and pattern matching. This is what I like to call the "copypasta code" level of learning. I want to be clear that I'm not knocking this type of learning or copypasta code. In fact, we'd better not call it "lower" at all -- it's foundational. And many experienced programmers or subject-matter experts will often have to relearn foundational tools to learn.

In both these paradigms, longterm memory building is prized at the foundational level. Built upon these skills, pattern matching and chaining information is formed. Then learning what something is NOT (analyzing, discrimination learning) starts to become helpful. For example, when I started learning a functional programming language for the first time after programming only on object-oriented languages, I was surprised how much it strengthened my understanding of OOP. Finally, when we have a good grasp of the basics, we can start to form mental models or concepts generally applicable across different types of examples. Finally, we can create. Honestly, I think there should be a final item with both of these hierarchies -- opinions. They should be a thing you can hold at the highest rung. Unfortunately, many ranks these much lower in their learning calculus.

While I definitely (and I assume most people do) interact with these hierarchies in very non-linear ways, they can be incredibly helpful when setting out to learn anything new. And they'll often help explain to me why, when learning Go for the first time for example, I couldn't right away start creating or solving complex problems in it.

Over the last year, in order to inch closer towards the top of these hierarchies, I've become reacquainted with some old enemies: quizzes and flashcards.

This is because I realized early on in my first year as an ops engineer that the more I knew about the tools as my disposal, the faster I could recognize the constraints of any given project I was assigned. This is because once you have knowledge (no expertise needed!) you can start to ask better questions. When you have good memory, it allows you to be more creative in solving problems.

I found success learning about the things that inhabit the ops universe in a couple ways:

## Practicing Retrieval

_Continuous development and testing for your brain!_

Simply re-reading material has been proven to not work. However, practicing retrieval of that material can. Retrieval is just recalling something from memory.

### Low stakes testing

Try testing yourself after you read something. Retrieval is proven to force the brain to make strong connections to concepts. While short term memory kind of sucks, our longterm memory is incredibly plastic. But don’t test yourself on things right away. Difficult learning leads to stronger memory. By spacing out your retrieval you make your brain strain more.

### Reflection

Writing about something after you learn it. Reflection helps consolidate ideas into longterm memory because it links them to experience we already have. It’s as simple as asking yourself what went well, could have gone better, could do next time.

## Memory Palaces

I’ve used memory palaces to remember concepts around networking, HTTP codes, linux features, and AWS services.

Builds on a cool feature many humans have called imagination inflation. This is the ability for us to imagine things so strongly we trick our brains into believing they are real and saving them in memory as real.

You just take a place you are already familiar with and place pieces of information throughout it while imagining something visceral or absurd in the place to make you remember. Like tarantulas passing notes in your living room to remind yourself about TCP.

## Constructing Mental Models

Mental models are the result of the extraction process where you take key concepts from new material and organize them. As we start to gather information about the ops universe, and monitoring systems for example, we are building up abstractions of those monitoring systems that will allow us to design other types of systems that aren’t exactly the same. Mental models, in other words, are what makes up expert intuition. 

## Having a Growth Mindset

The final memory tool that has been essential in this year is having, and working with people who have, a growth mindset.

There was a 2010 study done on 5th graders by the researcher Carol Dweck in New York where researchers gave them puzzles. After completing the puzzles, they told them either that they were very smart or that they worked very hard. They gave them another round of harder puzzles. The kids told that they worked hard did much better.

Here's a quote from the study:

> Emphasizing natural intelligence takes it out of the child’s control, and it provides no good recipe for responding to a failure.

Learning requires failure. Ops engineering definitely requires failure.

Surround yourself with people who believe this. I am lucky to work with a team the praises each other for working hard on difficult problems, not for being “smart” or naturally great engineers.

If any of these strategies are interesting to you, I took a lot of suggestions from [Make it Stick](https://www.amazon.com/Make-Stick-Science-Successful-Learning/dp/0674729013), a book about learning science.

## Final Note

As a final note, I want to say that while learning how to learn can be a great way for people new to any topic to level-up, it's also a powerful thing for anyone in a technical leadership position to embrace as well. First, it'll allow you to mentor and train new engineers faster. Second, recognizing the fundamental importance of pattern matching and copying should force us to make code bases, runbooks, and documentation that is kind and considerate towards newcomers. We are all constantly learning across different levels of understanding. We are all trying to take our learning to the level of craft. Understanding how we learning can help not only ourselves learn faster, but be more empathetic in general.

_I hope to share more learning tips and tricks as I come across them. Also, I'm using this blog as a sort of longform of reflection and retrieval, to help myself learn as well._