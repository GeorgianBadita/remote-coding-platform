# remote-coding-platform

- [remote-coding-platform](#remote-coding-platform)
  - [Purpose](#purpose)
  - [Background](#background)
  - [Goals](#goals)
  - [Non-Goals](#non-goals)
  - [Services](#services)
    - [User service](#user-service)
    - [Remote Coding Execution Service](#remote-coding-execution-service)
    - [Questions Manager Service](#questions-manager-service)
    - [Content Testing Service](#content-testing-service)
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
List of services for the Remote Coding Platform.

### User service
### Remote Coding Execution Service
This service will handle all code executions for the platorm. Its only purpose is to run the given code against
the given tests and save the submission in a DynamoDB database to be queried later.
It will expose the following api:
* Create a code submission
  * **URL**
    
    `/api/v1/submission`

  * Method

    `POST`

  * Data Params

    ```javascript
    {
      "language":"python",
      "code": "def return_string(s):\n\treturn s",
      "targetFunctionName": "return_string",
      "paramList": ["STRING"], 
      "tests": [
        {
          "input": [
            {"s": "YES"}
          ], 
          "output": {"s": "YES"}
        }
      ],
      "maximumExecTime": "1s"
    }
    ```
  * Success Response

    Code: 201 - CREATED
    Response Body:

    ```javascript
    {
      "submissionId": "12312dasd1",
      "hasError": false,
      "passedAll": true, 
      "results": [true, true, true, true, true, true, true],
      "outOfResources": false,
      "exitCode": 0,
      "outOfTime": false,
      "rawOutput": "----- Test Case 1 ---- ..."
    }
    ```
  * Error Response

    Code: 401 - UNAUTHORIZED
    Response Body:
     ```javascript
    {
      "error": "Not Authorized Entity"
    }
    ```

* Retreive a code submission
  * **URL**
    
    `api/v1//submission/{id}`

  * Method

    `GET`

  * URL Params
    `id=[string]`

  * Success Response

    Code: 200 - OK
    Response Body:

    ```javascript
    {
      "submissionId": "12312dasd1",
      "hasError": false,
      "passedAll": true, 
      "results": [true, true, true, true, true, true, true],
      "outOfResources": false,
      "exitCode": 0,
      "outOfTime": false,
      "rawOutput": "----- Test Case 1 ---- ..."
    }
    ```
  * Error Response

    Code: 401 - UNAUTHORIZED
    Response Body:
     ```javascript
    {
      "error": "Not Authorized Entity"
    }
    ```


* Create a simple code execution - given a piece of code return its output
  
  * **URL**
    
    `api/v1//execution`

  * Method

    `POST`

  * Data Params

    ```javascript
    {
      "language":"python",
      "code": "def return_string(s):\n\treturn s",
    }
    ```
  * Success Response

    Code: 201 - CREATED
    Response Body:

    ```javascript
    {
      "hasError": false,
      "outOfResources": false,
      "exitCode": 0,
      "outOfTime": false,
      "rawOutput": "----- Test Case 1 ---- ..."
    }
    ```
  * Error Response

    Code: 401 - UNAUTHORIZED
    Response Body:
     ```javascript
    {
      "error": "Not Authorized Entity"
    }
    ```


### Questions Manager Service 
### Content Testing Service

## Design Options

## Use Case Diagam
## Option 1 - O1
## Option 2 - O2
