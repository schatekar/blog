---
title: "Dear product managers, do not hold your team to their estimates"
published: true
excerpt: "It's impossible to come up with an estimate that is close to reality, specifically when the reality itself is not constant which is usually the case.
If you, as a product manager, fail to realise this and keep holding the team for their estimates, then they will learn to work around your behaviour by inflating the estimates or by cutting corners. Both are harmful to your product. So how do you deal with such situation without blowing your budget through the roof?"
tweet: "Dear product managers, do not hold your team to their estimates"
---

![Estimates are never correct]({{ site.url }}/images/estimation-billboard.jpg)

To all the product managers friends out there — if you keep holding your team to their estimates, one of the two will happen. Either they will find ways to work around your behaviour or you will end up with a product that is sub-optimal in quality. 
Estimates by definition are guesses. And they can be as correct or as wrong as any other guess. Closeness of an estimate to reality depends on a number of factors
1. Has the team worked on a feature like the one in question before?
2. How skilled is the team at using the tools and tech?
3. How experienced is the team in understanding the complexity of the business requirements?
4. Does the new work result in re-doing some of the previously done work?
5. How good is the team at working out #4?
6. How quickly can the team find out they are on the wrong path and how quickly can they recover?
7. Do the processes slow the team down?
8. If #7 is the case, does the team know the extent?

I am sure I have not covered everything here. But you get the gist — it’s impossible to come up with an estimate that is close to reality, specifically when the reality itself is not constant which is usually the case.
If you, as a product manager, fail to realise this and keep holding the team for their estimates, then they will learn to work around your behaviour by inflating the estimates or by cutting corners. Both are harmful to your product. So how do you deal with such situation without blowing your budget through the roof?

## Keep an eye on team's velocity
In an ideal scenario, the velocity of a team should increase over time, everything being constant. This is because team keeps getting better at understanding the domain and using the tools and the tech. If the velocity is going down or is constant then it's time to ask the right question.

## See if you are adding more complex features to the backlog or changing scope
Before you set out to ask the right questions, take a good look at your backlog to find out
1. If the recent features that the team delivered were more complex than the ones they delivered earlier
2. If the scope of features has changed after the initial estimate was provided

If the answers to above are positive then its worth knowing how the team felt about the change in complexity or scope. If nothing else, it will help build relationships

## Find out what caused velocity to go down
A lot of reasons can contribute to a low velocity. Have a chat with your team and understand the challenges they faced. Did they misunderstand a requirement? Did they develop something that was not in the scope? Help them understand the priority of the features by attaching business value to each feature. Sometimes it could be a simple and silly mistake but who does not make mistakes? The key is learning from the mistakes.

## Respect the practices that team follows
Some of the practices like TDD and DevOps result in significant cost investment at the beginning of the project and generally a higher ongoing cost of delivery. But remember, these practices help tremendously in our ability to deliver a quality software and turning around new features quickly. Our industry has learned in recent years what it means to go from development environment to production within hours than days or weeks. It is the practices like TDD and DevOps that make such speed of delivery possible. It comes at a cost, however, the key is to remember that even the efforts required for TDD and DevOps need to be estimated. Like any other estimate, these estimates are likely to go wrong as well.

## Understand that developers love upkeep of their code
Developers are continuously enhancing their coding skills. This means, every now and then, they would look at their old code and realise how it can be made better. Upkeep of code quality needs time investment and in some cases may bring the velocity down. In the absence of an understanding between the product manager and the team, developers would either ignore such enhancements and go on building tech debt that will eventually crumble the product down. Or they would just go ahead and invest time bringing down the velocity.
Engage with your team, understand why it is important to maintain code quality. Try to strike a balance between an acceptable code quality and velocity.

## And lastly remember this iron triangle of software quality
If you want your software at a low cost and delivered fast, then you are most likely to lose out on quality.

![Iron triangle of software quality]({{ site.url }}/images/quality-triangle.png)