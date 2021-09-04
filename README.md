# Table of Contents
1. [Introduction](#introduction)
1. [Business Architecture](#Business-Architecture)
   1. [Problem Statement](##problem-statement)
   1. [Use Cases](##use-cases)
   1. [Commentary](###Commentary)
1. [Application Architecture](#Application-Architecture)
    1. [Commentary](#comm)
1. [Installation Instructions](#Installation-Instructions)


# Introduction
This project illustrates the design process that I go through when architecting software. As such, this readme includes a lite set of documentation with commentary that explains the business problem being solved and my thoughts on the section at hand.

The documentation will only stay slightly ahead of the implementation within the code, so as to avoid [Big Design Up Front](https://en.wikipedia.org/wiki/Big_Design_Up_Front).

For readers looking for code deployment instructions, please [go to last section of this page](#Installation-Instructions).

# Business Architecture
## Problem Statement
Traditionally, trains run on set schedules that are optimised for maximum passenger capacity rather than flow of the individual. However, understanding what the optimal schedule for trains is requires analysing a large amount of data of previous journeys and trends. Furthermore, there are other factors that should be optimised such as the number of or size of carriages. These factors can be used in "What If" scenarios to improve the physical design of trains and railways.

There is another potential problem that is worth investigation to conclusively prove the optimal setup of a train service. Traditionally, the train's schedule dictates the timing of an individuals journey rather than the individual having agency over the process. Equating this to road traffic, the current model is equivalent of a bus whereas a method that prioritises the individual would be a taxi. Would an on-demand train service be better placed to meet the needs of the individual and at what cost?


## Use Cases
The initial set of use cases that need to be catered for are purposefully slim so as to be focused on demonstrating business value. Once value has been demonstrated, feedback from the solution can be used to drive future use cases and improvements.

The first set of use cases are:
| Actor      | Use Case |
| -----------| ----------- |
| Scheduler  | Customise scenarios to be simulated           |
| Scheduler  | Run a simulation using the specified scenario |
| Scheduler  | View the results of the simulation            |
| Scheduler  | Compare the results of multiple simulations   |

While there are many smaller related use cases, these are the main use cases that shape the design. The others are supplemental and support the implementation of these main use cases.

### Actors
#### Train Scheduler
The Train Scheduler (hereby known as Scheduler) is responsible for setting the schedule for each train and therefore improving the efficiency of the overall set up of the trains.


---
**COMMENTARY NOTE**

I would normally use images here to complement the text but since I'm using markdown and GitHub I decided to skip that for ease right now. I may come back and add them later.

As this process is theoretical, there is only a single actor for all of the use cases. However, this is common in the scenario of a startup (even within an existing company) where the first priority is to deliver and prove value fast so that a decision can be made as to whether it is worth investing more into the solution.

---


## Commentary

All business processes are there to solve a problem or exploit an opportunity. Clearly articulating the issue is the first step in being in a position to design a solution. Normally, this would be drawn out using some flavour of business architecture workshop to map the current or future business process, following whatever the participants are most familiar with e.g. Event Storming (preferred), Value Stream Mapping, Capability Mapping, Requirements Gathering. 

It is **vital** that the right technical people are involved in this discussion from the very beginning and that the business experts continue to be involved throughout the design process, which includes the creation and delivery of any solution ([creating software is a design process](https://www.extremeuncertainty.com/software-development-design-activity/#:~:text=Software%20development%20is%20not%20a%20manufacturing%20activity&text=That%20is%2C%20it%20is%20not,%2C%20DLLs%2C%20database%20schemas)). In the top performing companies, this iterative design and improvement process is owned by a Product or Feature team that continue to evolve the product throughout its lifespan.

At this stage, I believe it is important to map the business process in its most conceptual form, agnostic of any technology or current implementation details.

# Application Architecture
## Overview 
As all 4 of the stated use cases are conducted by the same user, are usually conducted in a sequence, and revolve around the same business domain, the application architecture will mirror this and only start with a single application that caters for all of the use cases.


## Commentary
At all stages, the simplest application architecture that meets the business needs and the team structure is the right choice. As the team structure is a single user and maintainer with no differentiator in non-functional requirements, there is no reason to adopt a microservices architecture. This design would impact the delivery timeframe of an MVP, which is the most critical factor in enabling us to effectively judge the value of a new application. However, still adhering to a coarse-grained separation of concerns will give the architecture the best compromise of extensibility and delivery speed.

# Installation Instructions
1. Clone the repository
2. Open the command line in the TrainSimulation folder
3. Run the command `docker build -t trainsim -f Dockerfile .`
4. Run the command `docker run -it --rm -p 8080:80 trainsim`
5. Access the API on `http://localhost:8080/`