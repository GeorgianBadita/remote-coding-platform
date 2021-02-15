# remote-coding-platform

- [remote-coding-platform](#remote-coding-platform)
  - [Purpose](#purpose)
  - [Background](#background)
  - [Goals](#goals)
  - [Non-Goals](#non-goals)
  - [Services](#services)
    - [User service](#user-service)
    - [Remote Code Execution Service](#remote-code-execution-service)
    - [Platform Manager Service](#platform-manager-service)
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
### Remote Code Execution Service
This service will handle all code executions for the platorm. Its only purpose is to run a given piece of code in a Docker container and return
the output of the execution.

It will consist of a server written using [FastAPI](https://fastapi.tiangolo.com/) and an worker which will use [Celery](https://docs.celeryproject.org/en/stable/getting-started/introduction.html).

The server will post code executions in a [RabbitMQ](https://www.rabbitmq.com/) task queue, and the worker will process each execution from the queue.
This design decision was taken with security in mind, as running code, directly on the server can have significant impact in cases, where bad intended users
may want to run fork bombs/infinite loops/malicious bash commands.

The server will expose the following API:

* Create a code evaluation - The server will evaluate the code and return data about the code correctness
  * **URL**
    
    `/api/v1/evaluations`

  * Method

    `POST`

  * Data Params

    ```javascript
    {
      "language":"python",
      "code": "def return_string(s):\n\treturn s {... code for unittesting the method}",
      "timeout": 2.1 
    }
    ```
  * Success Response

    Code: 200 - OK
    Response Body:

    ```javascript
    {
      "submissionId": "some-uuid",
      "hasError": false, 
      "results": [true, true],
      "out_of_resources": false,
      "exitCode": 0,
      "out_of_time": false,
      "raw_output": "----- Test Case 1 ----\n----- Test Case 2 ----"
    }
    ```
  * Error Response

    Code: 400 - BAD REQUEST
    Response Body:
    ```javascript
    {
      "detail": "Invalid test code format"
    }
    ```

    Code: 422 - VALIDATION ERROR
    Response Body:
    ```javascript
    {
      "detail": [
        {
          "loc": [
            "string"
          ],
          "msg": "string",
          "type": "string"
        }
      ]
    }
    ```

    Code: 500 - INTERNAL SERVER ERROR
    Response Body:
    ```javascript
    {
      "detail": "The server could not process the code execution"
    }
    ```

* Create a simple code execution - given a piece of code return its output
  
  * **URL**
    
    `api/v1//executions`

  * Method

    `POST`

  * Data Params

    ```javascript
    {
      "language":"python",
      "code": "print(\"Hello World\")",
      "timeout": 2.1
    }
    ```
  * Success Response

    Code: 200 - OK
    Response Body:

    ```javascript
    {
      "hasError": false,
      "out_of_resources": false,
      "exit_code": 0,
      "out_of_time": false,
      "raw_output": "Hello World\n"
    }
    ```
  * Error Response

    Code: 422 - VALIDATION ERROR
    Response Body:
    ```javascript
    {
      "detail": [
        {
          "loc": [
            "string"
          ],
          "msg": "string",
          "type": "string"
        }
      ]
    }
    ```

    Code: 500 - INTERNAL SERVER ERROR
    Response Body:
    ```javascript
    {
      "detail": "The server could not process the code execution"
    }
    ```


### Platform Manager Service 
### Content Manager Service

## Design Options

## Use Case Diagam
## Option 1 - O1
## Option 2 - O2
