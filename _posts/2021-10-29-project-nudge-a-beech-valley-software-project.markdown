---
layout: post
title: "Project Nudge: A Beech Valley Software Project"
categories: ProductDevelopment Staffing Recruiting Leading
date: 2021-10-29
blurb: "Beech Valley can be thought of as the gig economy for the accounting industry. We operate as a fairly lean team so how we approach executing work comes with that in mind.

Here’s how we ideated, planned, and executed one of our latest successful projects here at Beech Valley."
---

Beech Valley can be thought of as the gig economy for the accounting industry. We operate as a fairly lean team so how we approach executing work comes with that in mind.

Here’s how we ideated, planned, and executed one of our latest successful projects here at Beech Valley.

An important aspect of the work described here requires background on how our product works. Beech Valley has projects with clients and within each project is a hiring pipeline. Within each pipeline are a number of stages a candidate has to go through to get to the end goal: Hired or Disqualified. Something we noticed is that candidates often sit longer than expected in a certain stage of the pipeline. The goal of the project is to move people along the pipeline quicker so they are never stuck for too long (and that they reach an end state!).

## 💡 Ideation

The first step in our project lifecycle was determining the root issue. Why were people getting stuck in specific states? To identify the problem, we interviewed a handful of people on our internal team to help give us some clues.

We did three different 30-minute sessions where we had a product designer, an engineering lead (me) and an internal employee of our app sit down together for a chat. Our goal was to learn from the internal employee's workflow. The conversation would usually start with the engineer or product designer setting the initial context by asking something along the lines of "Walk us through a typical pipeline" and then asking questions along the way to tease out what’s happening, why it’s happening, and which steps we can take to fix the issue.

After the 30-minute session, the product development team would debrief and share some notes together until all sessions were completed. This gave us a much better idea of what was going on and at this point we could have a longer session on what we want to do to solve it.

In this case our engineering lead (me) took the reigns for this project and started a product design document outlining the scenarios we wanted to solve given the information we had learned. We scheduled some time as a team to talk through the design document and brainstormed how to solve the different scenarios. What was initially a smattering of individual solutions started taking shape into something more.

## 📄 Planning

At this stage, we now had clear goals for our project. We wanted to reduce time spent in each pipeline state. What we found out through ideation is that each pipeline state has an input and an output. The input and output can be owned by different people and requires action on their part in order to hand it off to the next person. Specifically, the people involved in our pipeline include the client (person who wants to hire someone), the consultant (person who wants to be hired), and an internal Beech Valley representative.

The primary pain point we uncovered from the interviews is that people simply needed a reminder that it was their turn to take action in a certain stage of the pipeline.

Knowing this, we created three phases to our project in the order of value we thought it would bring to the business. In addition if we got interrupted in our workflow we could shelve a phase until we could get back to it.

**Phase One**: We enable our internal team to know exactly when a stage was overdue so they could take action in the form of a reminder. No more rustling through notes, emails, or self created reminders.

**Phase Two**: We remind consultants when we have potential projects available for them through automated interest checks and reminders.

**Phase Three**: We give our clients a daily rundown of where their projects are at and if they need attention through an automated email digest.

## 💻 Execution

We immediately planned out and started Phase One. We had our product designer come up with some ideas about what the features we wanted could look like and agreed on a plan of action. The engineering lead (me) took the first pass at writing out a few tickets and then we held a planning discussion with the rest of the engineering team to make sure it was the approach we wanted to take.

An interesting point in our execution phase is that we didn't write out any tickets or designs for Phase Two or Three initially. We just had a general idea of how we wanted to approach them from our product design document. What this allowed our team to do was interweave some other projects in before we started Phase Two and Three.

In terms of tech used during execution, most of the code consisted of a bit of React magic, sprinkles of GraphQL API schema changes, a smattering of new Postgres queries using Objection.js, and a handful of background pg-boss jobs to calculate or send emails outside the request-response lifecycle. All of which were wrapped with a set of tests in jest to make sure it all worked. A neat thing about this project is that most of it is written in one monorepo where the frontend, api, and background jobs all live together using nx to manage both projects and shared libraries.

## Closing

One improvement we could have made in execution is in the first phase, we should have picked a few metrics to help us identify that we were accomplishing our goal and measuring it. This is something we did when we started on phase two and three and immediately put those up front to help us know if our changes were successful.

Here are the key results from our project.

🎉 Phase 1 took 31 stories and a lot of kudos from our internal team for making their lives easier.
<br />
🎉 Phase 2 took 12 stories and increased our response rates from consultants by 15%
<br />
🎉 Phase 3 took 9 stories and while still in progress of rolling out the feature we noticed an uptick in responses within thirty minutes after hitting a clients inbox.
