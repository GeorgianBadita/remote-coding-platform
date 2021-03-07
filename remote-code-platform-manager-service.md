# remote-code-platform-manager-service

- [remote-code-platform-manager-service](#remote-code-platform-manager-service)
  - [Description](#description)
  - [Atchitecture Diagram](#atchitecture-diagram)
  - [Storage and Accessibility Patterns](#storage-and-accessibility-patterns)


## Description

The Platform Manager service is the heart of Remote Coding platform, it will manage the state of each user in the platform, (i.e.) the problems solved by each user, together with its submissions on each problem.
This service will also support a playground where a user can freely execute pieces of code against given input.

## Atchitecture Diagram

## Storage and Accessibility Patterns


* Get problems on the platform (all/paginated). A problem contains: 
  * Problem name - String
  * Statement - String
  * Input example - String
  * Output example - String
  * Hints - String[]
  * Optimal complexity - String
  * Tags - String[]
  * Difficulty - String
  * Text cases - JSON[]
  * Input signature - String[] - list of types for the problem input
  * Output signature - Type of output
  * Supported languages - String[]
  * URLs to official solutions stored in S3 bucket - String[]
  * URLs to test code stored in S3 bucket - String[]

* Get problem by problem name
* Get user data by email. A user contains:
  * Source - Github/Google/Facebook - String
  * User - String
  * Email - String
  * URL to profile picture - String
  * Submissions - List of submissions
  * Solved problems - List of solved problems for user together with the submission id
  * Tried problems - List of partially/wrong submitted problems for the user together with submission id