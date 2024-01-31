---
title: My Opensource contributions
author: Yann POMIE
description: A list of (F)OSS projects I contributed to
date: 2024-01-30
---

> [!SUMMARY]- README!
> This page has been created in the context of a OpenSource class being a part of my [engineer training](https://www.polytech.umontpellier.fr/formation/cycle-ingenieur/devops/en-quelques-mots-do). 
> 
> Unless you are a recruiter, a teacher or REALLY interested in my OSS contributions, this page won't be much interesting :)

# Context

During my both my [engineering training](https://www.polytech.umontpellier.fr/formation/cycle-ingenieur/devops/en-quelques-mots-do) and my career, I got to contribute to Open Source Software (OSS), this page exists as a mean to list the projects I contributed to that will be updated. 

# Projects

- [Gama Platform](https://gama-platform.org/)

**Personally initiated projects**: 

- [RelFinderReformed](https://github.com/WoodenMaiden/RelfinderReformedAPI)
- [TimeCopSync](https://github.com/TimeCopSync)
## Contributions

### Gama Platform

| Repos/Organizations | Status | Stars | Stack |
| :----: | :----: | :----: | :----: |
| https://github.com/gama-platform<br>https://github.com/gama-platform/gama<br>https://github.com/gama-platform/gama.ppa<br>https://github.com/gama-platform/gama.distribution | Alive | 300 | Java, RCP Stack, Github Actions |

The [GAMA](https://gama-platform.org/) platform (_**G**IS **A**gent-based **M**odeling **A**rchitecture_) is an IDE for writing agent-based simulations. It involves a type of simulation where the logic is implemented at the level of the agents participating in the simulation. Each type of agent carries its own logic and interactions with other types of agents. For example, you can define that a predator-type agent roams in a plain and reproduces when it eats a prey-type agent.

GAMA offers an IDE as well as the GAML (**GA**ma **M**odeling **L**anguage) language to enable its users to carry out this kind of modeling. It is also possible to perform more complex modeling thanks to its plugin system, which allows for modeling in three dimensions as well as interacting with a database.

<iframe title="Gama 1.9.1 Release Video Trailer" src="https://www.youtube.com/embed/LvmNtsB1ytY?feature=oembed" height="113" width="200" allowfullscreen="" allow="fullscreen" style="aspect-ratio: 1.76991 / 1; width: 100%; height: 100%;"></iframe>

I started contributing to this project in the summer of 2023 when I went to the[ developers' laboratory](https://across-lab.org/) and I still am contributing to this day. I attempted to migrate the project managing from Maven to Gradle in order to improve it's CI/CD, however me and the other developers had a lot of trouble doing so, since the app is based on the Eclipse project, all the ecosystem relies on Maven, this task has been postponed.

Besides that I mostly work on the CI the packaging and the delivery of Gama here is a non-exhaustive list of task I did/am doing: 

- Cleaning up the CI scripts
- Setting up a Debian [repository hosted with cloud flare pages](https://github.com/gama-platform/gama.ppa)
- Setting up [CICD workflows](https://github.com/gama-platform/gama.distribution) to distribute the software under a variety of forms 


### RelFinderReformed (or RFR for short)

| Repos/Organizations | Status | Stars | Stack |
| :--: | :--: | :--: | :--: |
| https://github.com/WoodenMaiden/RelfinderReformedAPI<br>https://github.com/WoodenMaiden/RelfinderReformedFront | In development - Not Production Ready | 1 | NestJS, React |

RFR is an attempt to recreate a maintain a web Application named Relfinder which was used to determined the relations between two entities in a [RDF knowledge graph](https://en.wikipedia.org/wiki/Resource_Description_Framework). First made to replace the Relfinder instanced used by the [AgroLD platform](https://github.com/SouthGreenPlatform/AgroLD_webapp),  I made it OpenSource and as agnostic as possible so the semantic web community could use it. 

> [!Important] 
> As of today's date (2024-01-30) RFR is currently under a complete overhaul into a NestJS app, the project will be production-ready when PR [#16](https://github.com/WoodenMaiden/RelfinderReformedAPI/pull/16) will be merged.

![[rfr_test.png]]


### TimeCopSync

| Repos/Organizations | Status | Stars | Stack |
| :--: | :--: | :--: | :--: |
| https://github.com/orgs/TimeCopSync<br>https://github.com/TimeCopSync/timecopsync-crud<br>https://github.com/TimeCopSync/timecop-sync | In early development | 0 | Elixir, <br>Flutter,<br>Phoenix |

This project aims to provide an online hosting, synchronisation and integrations of a project named [timecop](https://github.com/hamaluik/timecop), an offline-first time tracker that I regularly use. This app allows you to register the time you spent on tasks related to projects, however it becomes cumbersome when you want to synchronize your timers across several devices, moreover it could have some interesting integrations with managing solutions like Jira, Notion and so on. This project is some kind of sandbox on which I experiment new languages like elixir and try to apply what I learned through my DevOps courses. 

![[timecop.png]]