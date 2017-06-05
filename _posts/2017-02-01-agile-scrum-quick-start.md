---
title: Agile Scrum Quick Reference
description: Agile Scrum Quick Reference
header: Agile Scrum Quick Reference
author: Rod
tags: [agile]
---
Implementing a software development process is rarely quick.  Processes typically take time to iterate to find what works best for the teams.  This post is meant to be a quick reference to key terms and ceremonies in an Agile/Scrum software development processes.


There are many aspects to an Agile/Scrum process.  For new teams that are implementing this process I think the best approach is to do as many of the ceremonies as possible then scale down based on team needs. The core pieces are the Sprint, Definition of Done and the User Story.

### Sprint
A Sprint at a high level consists of the following
- Iteration based (Typically 2 weeks)
- All of the work in the sprint is captured in user stories 
- Perform [Sprint Ceremonies](#sprint-ceremonies)

### Definition of Done
Defining what tasks need to be completed for the User Story to be done 
- Pull Request Approved
- Unit/Integration Tests
- QA Testing 
- Production Ready Code
- Merged

### User Story
User Stories typically follow the template below  

*Description:*  
	As a ```<type of user>```, I want ```<some goal>``` so that ```<some reason> ```   

*Acceptance Criteria:*  
	Functionality required that is used to confirm story is complete and working as intended.  It is not meant to be a full requirements document.  It should encourage some communication between product, dev and qa.

*Reference:* [Mountain Goat Software](https://www.mountaingoatsoftware.com/agile/user-stories)  

- - -

### Sprint Ceremonies

**Daily Standup**  

*When:* Everyday (15 min)  
*Who:* Team  

Each member of the team answers the following questions: 
1. What did you do yesterday?
2. What will you do today?  
3. Do you have any blockers?

**Sprint Planning**  

*When:*  First Day of Sprint  
*Who:* Team  

The team decides what user stories will be taken on in a sprint and commits to them.
1.  The Product Owner and/or Tech Lead gives a brief overview of the highest priority backlog items.  If there are last minute stories a quick grooming session occurs. The number of stories that is decided is based on velocity.
2. The stories are assigned and the team determines the tasks necessary to complete each product backlog item and estimates the ideal hours they need to finish each task.
3. Capacity planning is done and if any individual exceeds their capacity during the sprint, then the team collaborates to distribute the load or remove stories from the sprint.
4. Decide on what will be demoed and released at the end of the sprint

**Mid-Sprint Review**  

*When:*  Mid Sprint  
*Who:* Team  

Review how the stories that were committed to are doing.  
1. Review the burndown and discuss blockers
2. Confirm what will be demoed and released

**Backlog Grooming**  

*When:*  Mid Sprint or Until Backlog is groomed a couple of sprints out  
*Who:* Team  

User stories are reviewed to size, determine if a spike is necessary, or if more acceptance criteria need to be added.
1. The Product Owner and/or Tech Lead gives an overview of the highest ranked product backlog items that have not been sized.  Stories should be formatted using the User Story Template.
2. For each story the teams asks any questions and determines if additional acceptance criteria is needed.
3. The team determines the size of the stories relative to each other.
4. If a story is determined to large to be completed in a sprint it is broken done to smaller manageable stories.
5. The team suggests any new stories that could be added (ex. Tech Debt, New Feature)

**Retrospective/Demo**  

*When:*  Last Day of Sprint  
*Who:* Team  

Review how the sprint went and what was completed
1. Demo the features that have been completed in the sprint
2. Review the sprint metrics (# of Stories, Total Points, Completed vs Incomplete Stories)
3. Review previous retro action items
4. Retro exercise (Good vs Bad, Start Stop Continue)
5. Determine retro action items

**Discovery**  

*When:* As Needed  
*Who:* Product Manager and Tech Lead  

Management of the backlog, ideally creating stories multiple sprints out.
1. Create epics and user stories
2. Prioritize backlog before grooming
3. Gather additional requirements using story mapping

- - -

### Additional Concepts  

**Velocity**  
Velocity is the trend of total user points that can be completed in one sprint.  

**Burndown Chart**  
Burndown chart shows you how quickly stories are being completed over the course of one sprint.  

**Spike**  
Spikes are used as research stories to get a better understanding of functionality or research needed to properly size a user story.  

**Capacity Planning**  
Capacity planning calculates the number of hours a team member will be available during a sprint.  

**Sizing**  
Sizing is way of estimating a story taking into account the effort, complexity, and doubt.  Typically done using the Fibonacci sequence.  This is a good reference for [sizing and estimating](https://help.rallydev.com/sizing-and-estimates). 

**Task**  
Tasks are a further breakdown of the user story.

**Day to QA**  
Day to QA is done on the first day of the sprint and is a process in which the team estimates when a story will be ready for QA.  This exercise lets QA plan accordingly and is helpful to prevent stories from being piled up at the end of the sprint for testing.

- - -

### Getting Teams Engaged

I have found that, if not facilitated correctly, the backlog grooming and spring planning sessions are the meetings where the teams are less engaged.  What I have found that has helped is making these sessions more interactive where the whole team is involved.  

*Retrospectives*: A good approach is to use post it notes with a thought per note where each person would post there thoughts on the wall.  

*Backlog Grooming*: One approach is to pre-assign stories to the team prior to backlog grooming and allow them to confirm that a story has the correct acceptance criteria and enough knowledge to size the story. 


