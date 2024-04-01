---
title: Experimentation Team Vision
description: This remit is an org agnostic remit for how an organization is able to build and nurture a culture of experimentation.
weight: 4
---

## I. Purpose and Motivation
This document answers these questions: 

* “How might we concisely communicate and align on the goal, function, and direction of the experimentation program?”
* “What parts of the program are we working on to improve the volume and velocity of testing, who owns these initiatives, and what are they measured by?”

This document outlines the vision for broadly democratizing an experimentation culture at an organization, and to outline the mechanisms we will invest in to enable teams to embrace this culture. 

As an organization embraces a learning and data-informed approach to make customer-facing decisions, experimentation is and will continue to be key to our success. While experimentation is an umbrella term that encompasses decision science including causal inference modeling, MVP betas, pilots, quasi experiments and even qualitative research methods like design or copy or user test intervention analysis, this paper addresses the need for us to first develop a culture where we test with velocity in order to have quicker measurement and feedback to our work.

Various studies illustrate how experimentation has supercharged the growth of companies and subsequently led to a culture of innovation through localized decision-making, customer focus, and psychological safety around the idea of failure. Thus, developing this skill set and culture across our entire company will help us reap the same benefits. 

In previous organizations, over one year of testing, we’ve seen ~500K/month in estimated monetary returns for the ecommerce team with an iterative approach to testing over our home page, product pages, and cart. Through testing we’ve come to have a better understanding on the transactional intent and preferences of users on a product line level.

We have an opportunity to help other teams and everyone in the org to understand the value of testing and help them succeed with it to benefit similarly. To get there, we need to develop a culture that fosters a view that testing and failure are a necessity to change, rather than an impediment towards progress.

As a starting point, we recommend the formation of a consolidated Test and Learn team to ideate on and subsequently invest in Processes & Governance, Tools & Data and People & Skills to drive a comprehensive and holistic Culture & Strategy of experimentation at VMware. As experimentation reaches maturity through the organization, this team can become a center of excellence that advises and enables teams throughout the organization to test with autonomy.

This document describes our mission and tenets, mechanisms that we need to invest in to drive the culture, and how we will build on top of existing mechanisms to solidify this culture. 

Key Question: We can set up various mechanisms to enable teams to test more often, but likely need a function to incentivize every team to engage in testing through a centralized function. What mechanisms can we put into place for teams to adopt and embrace A/B testing?

## II. Mission and Tenets
As the trusted foundation to accelerate innovation, our organization meets customers where they are. We do this by investing in features and capabilities that effect and increase the company’s North Star [to be filled]. This team will help the org make the right investments by measuring the effectiveness of these endeavors, and shed light on which marketing campaigns, messaging, positioning, journeys, features, and capabilities benefit and resonate with the customer the most (and why). Consequently, our mission is to “Guide the org's decision-making ability through a culture of experimentation”. We will do this by nurturing a “Test Before Invest & Measurement” mindset, helping product and marketing teams strategize what to invest in next based on the measured incremental impact of their work.

Our Tenets:

1. We will provide the tooling and resources (people, process, and technology) to enable experimentation at scale
2. We will instill the culture of ‘fail fast, learn fast’ by focusing on process and learning as part of the success
3. We will demonstrate where testing leads to improvements in our customer engagement and experience
4. We will make experimentation as simple and accessible as possible (scoping, planning, implementing, reporting, iterating without slowing down velocity)

## III. Mechanisms we will invest in
The following describes the mechanisms we will need to initially invest in across three broad categories of (i) Tools, (ii) Process, and (iii) People to help Product Managers, Marketers and Engineers adopt experimentation and eventually become its champions. The following subsections describe the mechanisms that the Experimentation Squad believes are the most important across each of these categories. 

Key note: we will continue to periodically benchmark and track progress on these key mechanism pillars through a program benchmark gap finding analysis.


### Tools & Data

1. <ins>An experiment data management platform:</ins> that will serve as a single source of truth that captures all data - including links to test design, setup, documentation, analyses, results, etc.
The database is also the semantic data dictionary, the hub of metadata that creates reports and communication artifacts etc. It also is the system that structures the methodology of action.

2. <ins>Accurate analytics services and tooling:</ins>  Ensuring that test tooling and data analytics tooling works, and teams using these tools are educated on how to use them, how and when they should alert for issues, standardization of metrics for reporting to reduce chances of error, and a data dictionary to help teams contextualize how to use those metrics for test analysis 

3. <ins>Structured Idea Backlog:</ins> An idea entry form (per team) that allows each team to maintain a repository of ideas they want to test, and prioritize which tests to run in which order. Through linked activities, we’ll also be able to elaborate on iterate on previous experiments. 

4. <ins>Enhanced Reporting and Analyses:</ins> Marketing and Product teams need enhanced features such as statistical significance tests and calculations, and believe that the current solution can be enhanced. Analytics teams have an opportunity to enhance their dashboards and data tools to provide more self-serve support

5. <ins>Preventing conflicts across experiments:</ins> A mechanism to develop shared reporting to keep a pulse on which experiments are live and the ability to detect whether two or more experiments are in conflict at a point in time. 

### Processes & Governance
1. <ins>Experiment Process Documentation:</ins> Creating accessible, concise and clear documentation on what teams need throughout the entire experiment lifecycle will be key to widespread adoption of testing
2. <ins>Experiment Stage Gates:</ins> Defining clear one-way gate processes for approval, assessment, and sign-off on how long a test should run; defining the process for engineers - to democratize it into a process that can be easily adjusted by team
3. <ins>Experiment Playbook:</ins> A modular document containing each step’s owner, acceptance criteria between various steps in an experiment’s lifecycle. 
4. <ins>Prioritizing Testable Ideas:</ins> A mechanism to discuss good ideation frameworks, and provide tools to empower teams to come up with what they should run first. This process will be geared towards teams that are testing more already, and will help them double down on their efforts by hosting more formal curation meetings where teams can knowledge-share and can collaborate to prioritize which ideas should be tested first, and why.
5. <ins>Experimentation Retrospective:</ins> A mechanism that will help teams already experimenting. The retrospective will help teams (i) gauge how effective their tests were based on velocity of generated learnings, (ii) assess the percentage of wins/hypotheses that worked well and why, and (iii) discuss where they see room for improvement to further focus on high value experiments based on past learnings.

### People & Skills
1. Experimentation Owner - This individual will strategize tests and act as a resource to the organization as they evangelize testing and learning
2. Project Manager - This individual will initially align the process and flows for experiments through different teams.
3. Dedicated UX Designer - This individual will research, identify, and propose positive user engagements and flows
4. Front-End Developer - This individual will aid with the development of complex experiments.

## IV. Mechanisms gap analysis
An org specific mechanism and gap analysis should be conducted prior to the implementation of a program. This will identify where resources will be necessary. 

Key note: The team will continue to periodically benchmark and track progress on these key mechanism pillars through a [program benchmark](https://speero.com/experimentation-program-maturity-audit) gap finding analysis.

Example Analysis:
| Mechanism | Present  | What we will develop further | Owner |
|-------------------|-----------------|------|-------|
| Experiment Management Platform   | Jira        | Enhancing [tool] as the single source of truth for all things experimentation management related. We will also integrate [tool] and Target for a more seamless experience |       |
| Accurate Analytics Services and Tooling            | Metrics that the marketing and growth product teams use and trust     | (1) Standardization of metrics that we will evaluate across tests; (2) Data Dictionary that describes and contextualizes the metrics. Adobe Analytics |       |
| Preventing conflicts across experiments      | Manual assessment  | Experiment tagging and aggregation framework + predefined taxonomy of tagging |       |

## V. Process Flow

<img src="https://github.com/Officialyi/docsy/blob/main/content/en/docs/Internal%20Education/process_flow.png?raw=true">