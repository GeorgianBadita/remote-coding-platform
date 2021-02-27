# remote-code-excution-service 

- [remote-code-excution-service](#remote-code-excution-service)
  - [Description](#description)
  - [Architecture Diagram](#architecture-diagram)
  - [API](#api)
    - [Create a code evaluation - The server will evaluate the code and return data about the code correctness](#create-a-code-evaluation---the-server-will-evaluate-the-code-and-return-data-about-the-code-correctness)
    - [Create a simple code execution - given a piece of code return its output](#create-a-simple-code-execution---given-a-piece-of-code-return-its-output)

## Description

This service will handle all code executions for the platorm. Its only purpose is to run a given piece of code in a Docker container and return the output of the execution.

It will consist of a server written using [FastAPI](https://fastapi.tiangolo.com/) and an worker which will use [Celey](https://docs.celeryproject.org/en/stable/getting-started/introduction.html).

The server will post code executions in a [RabbitMQ](https://www.rabbitmq.com/) task queue, and the worker will process each execution from the queue.
This design decision was taken with security in mind, as running code, directly on the server can have significant impact in cases, where bad intended users may want to run fork bombs/infinite loops/malicious bash commands.

## Architecture Diagram

A detailed Architecture Diagram can be seen below:

![remote-code-execution-engine-diagram](https://i.ibb.co/vPw58N4/Remote-Code-Execution-Engine-1.png)

## API

The server will expose the following API:

### Create a code evaluation - The server will evaluate the code and return data about the code correctness
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

### Create a simple code execution - given a piece of code return its output
  
  * **URL**
    
    `api/v1/executions`

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

