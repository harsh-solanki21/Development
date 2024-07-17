# REST API

REST stands for:

- **RE**presentational
- **S**tate
- **T**ransfer
- **A**pplication
- **P**rogramming
- **I**nterface

REST APIs can be implemented over different protocols, but in most cases, REST APIs are implemented over HTTPS.

<br />

## Key Concepts

- REST refers to a group of software architecture design constraints that bring about efficient, reliable, and scalable systems.
- The 6 constraints of REST:

  1. Client-Server architecture
  2. Statelessness
  3. Cacheability
  4. Layered System
  5. Code on demand
  6. Uniform interface

- REST is a stateless protocol which means no client context or information (aka "state") can be stored on the server between requests.

<br />

## HTTP Methods

| Method  | Description                                                    |
| ------- | -------------------------------------------------------------- |
| GET     | Read information about the resource                            |
| POST    | Create a new resource                                          |
| PUT     | Check if resource exists then update, else create new resource |
| PATCH   | Always for updating a resource                                 |
| DELETE  | Delete the resource                                            |
| HEAD    |                                                                |
| OPTIONS |                                                                |

<br />

## URI Parameters

### Path Parameter

It is a variable in a URI path that helps in pointing towards a specific resource.

Example:
https://mystoreapp/customer/1
Here, 1 is Path Parameter (different parameter will point to different resources)
mystoreapp is DNS
customer is resource name

https://mystoreapp/customer/2/orders
It will show all the orders of customer 2
changing path parameter will change the resource that your path is pointing to

<br />

### Query Parameter

It is a variable in a URI path that queries/filters through a list of resources

https://mystoreapp/customers?name=abc
Here, name=abc is Query Parameter

<br />

## HTTP Status Codes

### 1xx - Information

Used to inform a client status of the server. 1xx status codes are rarely encountered.

### 2xx - Success

- 200 OK
- 201 Created
- 204 No Content (means server processed the request but returned no content)

### 3xx - Redirection

- 301 Moved Permanently
- 302/303 Found at this other URL
- 307 Temporary redirect
- 308 Resume incomplete

### 4xx - Client Error

- 400 Bad request
- 401 Unauthorized
- 403 Forbidden
- 404 Not found
- 405 Method not allowed

### 5xx - Server Error

- 500 Internal server error
- 502 Bad gateway
- 503 Service unavailable
