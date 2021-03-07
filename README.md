# remote-coding-platform

- [remote-coding-platform](#remote-coding-platform)
  - [Purpose](#purpose)
  - [Background](#background)
  - [Goals](#goals)
  - [Non-Goals](#non-goals)
  - [High Level Architecture](#high-level-architecture)
  - [Services](#services)
    - [User service](#user-service)
    - [Remote Code Execution Service](#remote-code-execution-service)
    - [Platform Manager Service](#platform-manager-service)
      - [Stored Data and Accesibillity Patterns](#stored-data-and-accesibillity-patterns)
    - [Content Testing Service](#content-testing-service)

## Purpose

This document aims to present the design for an online remote code executinon platform called **Code Run**, where users will be able to solve various algorithmic problems and create/participate in online contests alongside other users.

## Background

As a user of multiple *Coding platforms* such as ([Codeforces](https://codeforces.com/), [Leetcode](https://leetcode.com/), [AlgoExpert](https://www.algoexpert.io/)), I have been wondering how these platforms work internally, so I
decided to onboard on the journey of creating one myself. I also noticed that some of these platforms have some issues regarding UI/UX or exposing/presenting the results to the user so while designing this application I will try to solve some of these issues.

## Goals
1. Data storage willl be NoSQL - DynamoDB
2. Application infrastructure will be hosted using AWS
3. Frontend technology will be React
4. AuthN/AuthZ willl be handled by a 3rd party using Oauth2.0 (Facrbook, Google, Github)
5. The code execution will be done using containerization (Docker or Linux Containers)
6. Users will be required to authenticate before subimtting any code to the platform (for security reasons)

## Non-Goals

1. No contest creation/participation capability will be considered for this version of the application
2. No CDNs will be considered for now, I may think of using one in the future

## High Level Architecture

  The following diagram provides an idea of the high level arthitecture of the platform

![architecture-diagram](https://i.ibb.co/7GSLx2D/Remote-Code-Execution-Engine.png)

## Services

List of services for the Remote Coding Platform.

### User service
### Remote Code Execution Service
This service will handle all code executions for the platorm. Its only purpose is to run a given piece of code in a Docker container and return the output of the execution.

A more detailed description of this service can be found [here](./remote-code-execution-service.md)


### Platform Manager Service
This service will manage the state of each user in the platform, (i.e.) the problems solved by each user, together
with its submissions on each problem.
This service will also support a playground where a user can freely execute pieces of code against given inputs.

A more detailed description of this service can be found [here](./remote-code-platform-manager-service.md)

#### Stored Data and Accesibillity Patterns


### Content Testing Service

