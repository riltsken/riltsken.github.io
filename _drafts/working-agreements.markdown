---
layout: post
title: "Working Agreements"
categories: SoftwareDevelopment WorkingWithTeams
blurb: ""
---

[DaveHKing]: http://wwww.davehking.com/

Working Agreements
-----

These were created by Dave H King, a former coworker.

With several workstreams across three locations, teams must have a shared understanding of how merging and code release happens.  This page documents the working agreements that team members must operate under when merging code into the mainline master branch.

Releasing a New Product
=====
This next section refers to the "Reach Release Process", a higher quality of CI/CD service for certain types of changes.  It should be used when the release of a feature into production is time critical or the release of a feature is likely to have a higher degree of impact to the automated testing pipeline.

Traditional CI/CD on Reach follows an hourly "bus" schedule.  Anyone can merge at any time and those changes will go to preproduction at the start of the next hour.  The "Reach Release Process" involves one team "owning" preproduction for a period in order to expedite a change and lower the amount of noise that sometimes occurs when multiple members changes integrate at the same time.

(The need for an expedited class of service in releases does indicates an underlying defect with our testing and release processes.  We should continue to work to improve these.)

__Agreement__: Before releasing a feature to all users in production, the feature should be released in preprod and staging first, followed by a run of the acceptance tests.
__Rationale__: New code may interact with feature flags in unforeseen ways.  Tests in preproduction and staging will find bugs that could have been missed before customers see them in production.

__Agreement__: Features are only released in the morning (prior to noon).
__Rationale__: It is easier to release during periods of low team, customer, and operational activity.  Releases that happen when the team is at full energy are more likely to succeed in the event that any unforseen event occurs.

__Agreement__: Releases are present on the Reach Release Calendar.
__Rationale__: To lower team confusion, one feature is released per day.  Using the Reach Release Calendar ensures that other teams are aware when preproduction will be "locked" to release a feature and prevents overlap.

__Agreement__: Send an email to reach-dev by noon the day before the release letting the entire team know what you are releasing and what to do (or not do).
__Rationale__: Team members need notification ahead of time whether preproduction/staging will be "locked" to release a feature the following morning.

__Agreement__: Send a note to reach-dev letting everyone know the release is complete
__Rationale__: Lets folks know to carry on with normal operations, notifies the project manager to send an update to any external parties as needed.

During Code Development
=====
__Agreement__: All changes to the master branch are done through Github pull requests and require review before being merged.
__Rationale__: Standard development practice for ensuring code quality

__Agreement__: All merges to master branch use Github 'green button'
__Rationale__: Green button does a no-FF merge and makes it easy to revert in the case of unexpected behavior.

After a Code Merge
=====
Merging code is the first step to the pipeline.  All code should be treated the same, even changes to a README require the same process.  What may be obvious to you may not be obvious to other team members and we are trying to avoid asking team members to make the judgement call "this might affect X because of ...".

__Agreement__: The Reach subteam who has a merged pull request is responsible for seeing it through the pipeline to production.
__Rationale__: Other team members across other workstreams are not able to understand the impact or context of every pull request.

__Agreement__: (When things do not work expectedly on preprod and staging)
If a merge does not work (from a user perspective) on preproduction or staging, the pull request must be fixed or reverted before the next scheduled preprod deploy (currently hourly).
If a merge breaks an acceptance test in preproduction or staging, the issue may be fixed later and be marked on the test failure spreadsheet.
__Rationale__: Preproduction and staging are a shared environment.  If broken it affects the ability of other teams to release code (include potentially critical bug fixes).  Attempting to 'hotfix' real problems over multiple hours blocks this resource from being used by other teams.  Acceptance tests failures are acceptable as long as an action item to follow up is taken and communication is done to other teams on the project.

After a Production Deploy
=====
Good job!  Code has been deployed to production.

__Agreement__: Team members are expected to be available for 1 hour after a production deploy of their code.
__Rationale__: Infrequently changes as a result of a production deploy requires team response.  Team members responsible for code changes have the most understanding of what might have been affected.

__Agreement__: Production deploys happen during team business hours (8am - 5pm Eastern) and only when a member of the subteam tasked for application support (in March 2014 this is Reach Yellow Team) is available.
__Rationale__: Infrequently production deploys cause issues that require team response.  Sometimes team response requires knowledge of the infrastructure in order to triage production issues and communicate out to the rest of the organization.  For this reason merges and deployments do not happen when Blacksburg teams are out of the office.