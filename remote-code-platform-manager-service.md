# remote-code-platform-manager-service

- [remote-code-platform-manager-service](#remote-code-platform-manager-service)
  - [Description](#description)
  - [Atchitecture Diagram](#atchitecture-diagram)
  - [Storage and Accessibility Patterns](#storage-and-accessibility-patterns)
  - [DynamoDB Tables](#dynamodb-tables)
    - [Users Table](#users-table)
    - [Questions Table](#questions-table)


## Description

The Platform Manager service is the heart of Remote Coding platform, it will manage the state of each user in the platform, (i.e.) the questions solved by each user, together with its submissions on each question.
This service will also support a playground where a user can freely execute pieces of code against given input.

## Atchitecture Diagram

## Storage and Accessibility Patterns


* Get questions on the platform (all/paginated). A question contains: 
  * Questsion name - String
  * Statement - String - Markdwon format
  * Hints - String[]
  * Optimal complexity - String
  * Tags - String[]
  * Difficulty - String
  * Test cases - JSON[]
  * Input signature - String[] - list of types for the question input
  * Output signature - Type of output
  * Supported languages - String[]
  * URLs to official solutions stored in S3 bucket - Map
  * URLs to test code stored in S3 bucket - Map

* Get question by question name
* Get user data by email. A user contains:
  * Source - Github/Google/Facebook - String
  * User - String
  * Email - String
  * URL to profile picture - String
  * Submissions - List of submissions
  * Solved questions - List of solved questions for user together with the submission id
  * Tried questions - List of partially/wrong submitted questions for the user together with submission id
* Update user data based on email

## DynamoDB Tables

The following DynamoDB tables will suppory my usecases for the coding platform:

### Users Table
Users table contains data about users and submissions for each user

![users-table](https://i.ibb.co/CwfbQbv/Coding-Platform.png)

### Questions Table

Questions table contains data about the paltform questions and official solutions
![questions-table](https://i.ibb.co/s1JD0x4/Questions.png)