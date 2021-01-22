# remote-coding-platform

- [remote-coding-platform](#remote-coding-platform)
  - [Purpose](#purpose)
  - [Background](#background)
  - [Goals](#goals)
  - [Non-Goals](#non-goals)
  - [Services](#services)
    - [User service](#user-service)
    - [Remote Coding Execution service](#remote-coding-execution-service)
    - [Questions manager service](#questions-manager-service)
  - [Design Options](#design-options)
  - [Use Case Diagam](#use-case-diagam)
  - [Option 1 - O1](#option-1---o1)
  - [Option 2 - O2](#option-2---o2)

## Purpose

This document aims to present the design for an online remote code executinon platform called **Name**, where users will be able to solve various algorithmic problems and create/participate in online contests alongside other users.

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

## Services

### User service
### Remote Coding Execution service
### Questions manager service 

## Design Options

## Use Case Diagam
## Option 1 - O1
## Option 2 - O2