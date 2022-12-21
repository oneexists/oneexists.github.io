---
layout: post
title: "Introduction to DevOps Core Values"
author: skylar_lynner
categories: [ devops ]
---

## First, Some Background

The practices proposed by DevOps can be integrated into a wide variety of teams to assist in
unifying development and operations from teams of developers, front-end, and QA to system,
network, and database admins. Creating a unified culture across these various teams allows
for easier communication, greater awareness of the bigger picture, and resolves conflicting
goals in the software development lifecycle.

Some results that can be expected from adopting a DevOps approach include more frequent
deployment, shorter lead times, fewer failures, and faster recovery from errors. This is
achieved by involving teams throughout the lifecycle from design and development to
production support.

## DevOps Core Values

The starting point of DevOps is understanding its values. These values are modeled using
the acronym CAMS.

**CAMS model: Culture, Automation, Measurement and Sharing**

This foundational concept drives the approaches taken to achieve the goal of allowing
teams to participate together in the various areas of concern addressed from design
through production of a service.

### Culture

Behavior drives culture, so it is important to intentionally shape culture in a way that
allows for effective communication. Some practices that can be implemented to assist in
the culture formation include
[blameless postmortems](https://www.atlassian.com/incident-management/postmortem/blameless),
transparent uptimes, which emphasizes the importance of communication during failures, and
recognizing [Conway's Law](https://www.atlassian.com/blog/teamwork/what-is-conways-law-acmi).

Following communication guidelines during postmortem communication assists in creating
a culture where teams are able to easily communicate with others about concerns that
arise. While this is especially important when addressing failures effectively, the
open floor created during this time shapes the wider culture to create an ease when
issues are recognized at any point. Creating an environment where these concerns can
be voiced allows for earlier recognition of potential issues, which results in faster
potential resolution measures.

Creating a culture of proactive communication through addressing transparent uptimes
encourages honesty and openness about existing concerns. While it may be tempting to
brush things under the rug when they are going wrong, this openness of communication
about issues builds trust between members and teams by providing a central location
for this type of communication.

Understanding the connection between communication structures and its effect on system
design, addressed within Conway's Law, creates a framework for understanding that
failures within communication do not end at the single point of communication, but
instead will be seen throughout the work being done by the team or organization.
Providing a standard for processes, management and communication allows for breaking
down any current barriers and results in improved overall outcomes.

Some teams implement organizational changes when implementing DevOps. This change
should not involve simply creating a "DevOps" job title, but instead should focus
on concerns such as breaking down team barriers to allow sharing of work, opening up
teams while maintaining a small group of core members, and possibly the addition of
push notifications into chat groups for events such as repository commits, builds,
and deployments.

### Automation

For many, automating processes will provide a tangible touch point of the practices being
implemented. This forms the basis of automation being the accelerator that provides
benefits of DevOps. An important concern when considering automation opportunities is the
refrain often sighted as "people over processes over tools." This is a reminder of the
hierarchy of concerns when implementing automation. It is tempting to scour the
marketplace for tools that appear to be helpful, but this approach ignores the people and
processes involved in implementing any of the tools selected.

The shift needed when considering opportunities for automation comes from starting
with current concerns of the people that would be using the tools, then working up to
evaluate the processes that could be automated. This insight can be used as information
to inform the research of which tool may be useful in resolving the identified concerns.

When reframing automation in this way, it becomes more clear that it is a strategy for
providing control over systems and applications. Implementing automation in ways that
allow for CI/CD, infrastructure as code, creating repeatable processes, and continuous
improvement are all ways in which processes can be improved to result in greater
outcomes.

### Measurement

Integrating measurement strategies and practices is a core concept with both Lean and
Agile methodologies, so it likely isn't a surprise that it is a value within implementing
DevOps as well. When done well, it provides a holistic insight that engages the team
in seeing the progress towards the overall goal of the project.

This aspect of the DevOps values includes some recommendations for considerations when
implementing measurement techniques and defining the results to be provided. The core
considerations when deciding what to include in measurement metrics are the Mean Time to
Recovery (MTTR), cycle time, costs, revenue and employee satisfaction.

These focuses when defining measurement criteria help with identifying the outcomes of
the practices and work being done. The ability to improve recovery times and cycle time
reflect the ability of the teams to effectively resolve issues as they arise and to
reduce lead times. Measuring the costs and revenue resulting from the work being done
provides oversight into the bottom lines of the goals in the accomplishment of goals.
Additionally, understanding the overall employee satisfaction provides a measurement
that indicates the health of the communication structures being implemented and to
identify concerns earlier rather than later.

### Sharing

The goal of sharing is to create an openness and transparency that reflects the cultural
shift being created with implementing DevOps values. This often includes sharing
responsibilities between teams and having members learn more about each other's daily
tasks. Focusing on implementing kaizen, or the focus on discrete and continuous improvement,
can provide a guide for finding areas that can be shared between team members.

While other areas more clearly assist in providing a feedback loop, such as sharing of
measurement outcomes, the work done to increase sharing in this way provides a tangible
change in job responsibilities that implements another level of increasing feedback. This
shift identifies areas where efficiency can be improved and increases an individual's ability
to contribute to assisting with a wider range of concerns.

Practices such as attending meetings across teams and broadening skill sets not only
contribute to the ability of teams to communicate with each other, but aides in their
ability to resolve issues without the need to rely on a single team, or even worse, a
single team member.

## Conclusion

Adding a broader perspective of the interactions between teams by implementing a DevOps
culture provides a space where teams are able to increase their communication, productivity,
and share responsibilities in a way that helps them gain insight in broader objectives.
Creating a culture that emphasizes communication, higher quality outcomes, and can quickly
respond to adversity allows for teams that are prepared for the inevitable difficulties
involved in managing project complexity.

For further insight into how DevOps fits into Agile Development methodologies, a summary
of my capstone presentation can be found
[here](https://oneexists.github.io/agile-and-devops/) that breaks down the Agile Development
lifecycle to show how DevOps can be used to create effective meetings, inform iterative and
incremental development, inform retrospectives, and build a new team culture.

## Resources

- [DevOps Foundations Course by Ernest Mueller and James Wickett](https://www.linkedin.com/learning/devops-foundations/development-and-operations-2?autoplay=true&contextUrn=urn%3Ali%3AlyndaLearningPath%3A5a724ea6498e02ebfd8de952&u=58636153)
- [Atlassian: Blameless Postmortems](https://www.atlassian.com/incident-management/postmortem/blameless)
- [Atlassian: Conway's Law](https://www.atlassian.com/blog/teamwork/what-is-conways-law-acmi)
