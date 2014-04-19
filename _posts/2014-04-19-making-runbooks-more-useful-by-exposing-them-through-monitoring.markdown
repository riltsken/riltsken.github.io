---
layout: post
title:  "Making runbooks more useful by exposing them through monitoring"
categories: DevOps Infrastructure Monitoring
blurb: "As mentioned in a previous post about our server message of the day (motd) we manage enough infrastructure that our team needs ways for being able to share tribal knowledge on how to fix issues. In Particular when we have monitoring alarms that kick off any of our team members should be able to take action on the alarm regardless of level, however, our team operates with so many different technologies it is difficult for any one person to be an expert in all of them."
---

[servermotd]: /devops/infrastructure/2014/03/16/how-server-message-of-the-day-improved-our-devops-team.html
[1_description]: http://b7cc86bc05773bcecd41-4057535a55b255b6cbfb486a61b5692d.r49.cf1.rackcdn.com/node_description.png
[2_actions]: http://b7cc86bc05773bcecd41-4057535a55b255b6cbfb486a61b5692d.r49.cf1.rackcdn.com/context_and_actions.png
[3_irc]: http://b7cc86bc05773bcecd41-4057535a55b255b6cbfb486a61b5692d.r49.cf1.rackcdn.com/irc_example.png
[tribal]: http://en.wikipedia.org/wiki/Tribal_knowledge
[runbooks]: http://en.wikipedia.org/wiki/Runbook
[pagerduty]: https://www.pagerduty.com/


In the [Server Message Of The Day (MOTD) post][servermotd], I mentioned the importance of sharing [tribal knowledge][tribal] across teams on fixing infrastructure issues. When any of our monitoring alarms kick off, any team member should be equipped to take action on the alarm, but we operate with so many different technologies that no one person could possibly be an expert in all of them. Most operations teams create [runbooks][runbooks] for common tasks, but we took it one step further and created runbooks for every alarm in our system. They don't exactly cover every possible reason for an alarm triggering, but will always help to provide context for someone that doesn't regularly deal with that subsystem.

Our runbooks are composed of the node's title and definition, its role in the system, and important config files. After that block is a section for all the system's monitoring alerts and what actions you can take to investigate or fix them. This is one of the runbooks for Cassandra:

![A description of the nodes role and configuration files][1_description]
![The actions we expect someone to take when initially debugging an issue when that alarm triggers][2_actions]

Triggered alarms link the runbook
-----------

We use IRC for team communication since we're all distributed. The alerts will stream into the channel via bot with direct links to the runbooks and every triggered alarm. While we do have a proper escalation path through [PagerDuty][pagerduty], this keeps the whole team aware of issues and gives anyone an easy path for investigation and action.

![One of the ways people get notified of issues and a link to the runbook for what to do][3_irc]
