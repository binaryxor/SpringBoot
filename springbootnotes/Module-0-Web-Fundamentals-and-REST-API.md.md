# Module 0: Web Fundamentals and REST API Basics

## 1. Client-Server Architecture

### Client
A client is an application or device that requests a service or resource from another computer.

Examples:
- Web browser
- Mobile application
- Desktop application
- Postman

### Server
A server is a computer or software application that receives requests, processes them, and sends responses.

A server can also communicate with databases to retrieve or store information.

**Example:**

When a user opens an employee management application:

1. The client sends a request to the server.
2. The server processes the request.
3. The server communicates with the database if required.
4. The database returns the requested information.
5. The server sends a response to the client.

---

## 2. HTTP and HTTPS — How Applications Communicate

### HTTP

HTTP stands for **Hypertext Transfer Protocol**.

It is a set of rules that allows a client and server to communicate with each other.

### HTTPS

HTTPS stands for **Hypertext Transfer Protocol Secure**.

It is the secure version of HTTP. The major difference is encryption using TLS (Transport Layer Security).

### URL

URL stands for **Uniform Resource Locator**.

It identifies the location of a resource.

Example:

```text
https://example.com:8080/employees
```

### Port

A port identifies a particular communication endpoint on a machine.

Example:
- HTTP: Port 80
- HTTPS: Port 443
- Spring Boot: Port 8080 (default)

---

## 3. HTTP Methods and Status Codes

### HTTP Methods

HTTP methods tell the server what action the client wants to perform on a particular resource.

| HTTP Method | Purpose | Example |
|---|---|---|
| GET | Retrieve data | Get all employees |
| POST | Create data | Add an employee |
| PUT | Replace existing data | Update an employee |
| PATCH | Partially update data | Update employee salary |
| DELETE | Delete data | Remove an employee |

**Important:** Soft delete is not an HTTP method. It is an application-level deletion strategy, generally implemented using PATCH or DELETE.

### Safe HTTP Method

A safe HTTP method is one that is intended to retrieve information without changing the server's application state.

### Idempotent Method

A method is idempotent if performing the same request multiple times has the same intended effect on the server as performing it once.

| Method | Safe? | Idempotent? |
|---|---|---|
| GET | Yes | Yes |
| POST | No | No, generally |
| PUT | No | Yes |
| PATCH | No | Not necessarily |
| DELETE | No | Yes |

**Example of Idempotency:**

Consider this request:

```http
DELETE /employees/101
```

First request: Employee 101 gets deleted.

Second request: Employee 101 is already deleted.

Both requests result in the same intended server state: employee 101 does not exist.

Therefore, DELETE is idempotent.

---

## 4. HTTP Status Codes

Whenever a client sends a request, the server sends a response.

The response contains a status code that tells the client what happened.

Example:

```http
HTTP/1.1 200 OK
```

### Status Code Categories

| Category | Meaning |
|---|---|
| 1xx | Informational |
| 2xx | Success |
| 3xx | Redirection |
| 4xx | Client Errors |
| 5xx | Server Errors |

### 4.1 Success Codes (2xx)

| Code | Meaning | Example |
|---|---|---|
| 200 | OK | Successfully retrieved employee |
| 201 | Created | Successfully created employee |
| 202 | Accepted | Request accepted for processing |
| 204 | No Content | Successfully deleted employee |

### 4.2 Redirection Codes (3xx)

| Code | Meaning |
|---|---|
| 301 | Moved Permanently |
| 302 | Found (Temporary Redirection) |
| 304 | Not Modified |

### 4.3 Client Error Codes (4xx)

| Code | Meaning | Example |
|---|---|---|
| 400 | Bad Request | Invalid request data |
| 401 | Unauthorized | Authentication required or failed |
| 403 | Forbidden | User lacks permission |
| 404 | Not Found | Employee doesn't exist |
| 405 | Method Not Allowed | Unsupported HTTP method |
| 409 | Conflict | Duplicate or conflicting resource |
| 415 | Unsupported Media Type | Unsupported request content type |
| 422 | Unprocessable Content | Request content cannot be processed |
| 429 | Too Many Requests | Rate limit exceeded |

### 4.4 Server Error Codes (5xx)

| Code | Meaning | Example |
|---|---|---|
| 500 | Internal Server Error | Unexpected application exception |
| 501 | Not Implemented | Server doesn't support required functionality |
| 502 | Bad Gateway | Gateway receives an invalid upstream response |
| 503 | Service Unavailable | Server temporarily unavailable |
| 504 | Gateway Timeout | Upstream server doesn't respond in time |

---

## 5. HTTP Request and Response Structure

### HTTP Request

An HTTP request is a message sent by a client to a server asking it to perform an operation.

There are four important components:

1. Request Line
2. Request Headers
3. Blank Line
4. Request Body (optional)

### 5.1 Request Line

Example:

```http
POST /employees HTTP/1.1
```

| Component | Value | Meaning |
|---|---|---|
| Method | POST | What operation to perform |
| Request Target | /employees | Which resource |
| HTTP Version | HTTP/1.1 | Protocol version |

### 5.2 Request Headers

Headers provide additional information about the request.

Example:

```http
Host: localhost:8080
Content-Type: application/json
Accept: application/json
Authorization: Bearer eyJhbGciOi...
```

| Header | Purpose |
|---|---|
| Host | Identifies the target host |
| Content-Type | Tells the server what format the request body is in |
| Accept | Tells the server what response format the client can understand or prefers |
| Authorization | Used to send authentication credentials or tokens |
| User-Agent | Identifies the client software |
| Cookie | Sends cookies to the server |
| Cache-Control | Provides caching directives |
| Origin | Identifies the origin of a request |
| Accept-Language | Indicates preferred response language |

### 5.3 Request Body

Contains the actual data that the client sends to the server.

Example:

```json
{
    "name": "John",
    "email": "john@example.com",
    "salary": 50000
}
```

---

### HTTP Response

An HTTP response is a message sent by the server to the client after processing a request.

It contains:

1. Status Line
2. Response Headers
3. Blank Line
4. Response Body (optional)

### 5.4 Status Line

Example:

```http
HTTP/1.1 201 Created
```

| Component | Meaning |
|---|---|
| HTTP/1.1 | Protocol version |
| 201 | Status code |
| Created | Status description |

### 5.5 Response Headers

Response headers provide additional information about the server's response.

Example:

```http
Content-Type: application/json
Content-Length: 85
Cache-Control: no-cache
```

| Header | Purpose |
|---|---|
| Content-Type | Format of response body |
| Content-Length | Size of response body in bytes |
| Cache-Control | Caching instructions |
| Set-Cookie | Sends cookies to the client |
| Location | Identifies a resource location, often after creation or redirection |
| Access-Control-Allow-Origin | Indicates permitted origins for CORS |

### 5.6 Response Body

Contains the actual information returned by the server.

Example:

```json
{
    "id": 101,
    "name": "John",
    "email": "john@example.com",
    "salary": 50000
}
```

---

## 6. JSON (JavaScript Object Notation)

JSON stands for **JavaScript Object Notation**.

It is a lightweight data-interchange format used to exchange information between applications.

Example:

```json
{
    "id": 101,
    "name": "John",
    "department": "IT"
}
```

JSON is commonly used in REST APIs to exchange information between clients and servers.

---

## 7. REST API Fundamentals

### API

API stands for **Application Programming Interface**.

An API is a mechanism that allows two software applications to communicate with each other through a defined interface.

### REST

REST stands for **Representational State Transfer**.

It is an architectural style used to design network-based applications.

It defines a set of principles for how clients and servers should communicate.

When an API follows REST principles, we commonly call it a **RESTful API**.

---

## 8. REST Architectural Constraints

REST defines six architectural constraints.

### 8.1 Client-Server Architecture

The client and server should have separate responsibilities.

- Client handles the user interface.
- Server handles business logic and data processing.

### 8.2 Statelessness

Statelessness means the server does not store client session state between requests as part of the REST interaction.

Every request must contain all the information required to process it.

For example, an authenticated request may include a JWT token:

```http
GET /employees
Authorization: Bearer <JWT_TOKEN>
```

The server uses the token to identify and authenticate the user.

### 8.3 Cacheability

REST responses should indicate whether they can be cached.

Caching means temporarily storing frequently accessed information so that it can be retrieved faster.

Benefits:
- Reduces server load.
- Improves response time.
- Reduces unnecessary network communication.

### 8.4 Uniform Interface

This constraint means REST APIs should provide a consistent way of interacting with resources.

For example:

```http
GET /employees
GET /employees/101
POST /employees
PUT /employees/101
DELETE /employees/101
```

Resources are identified using URLs, and HTTP methods define the operations.

### 8.5 Layered System

A client doesn't need to know how many internal components exist between itself and the server.

For example:

```text
Client
   |
Load Balancer
   |
API Gateway
   |
Application Server
   |
Database
```

The client communicates with the API without needing to understand the internal architecture.

### 8.6 Code on Demand (Optional)

The server can send executable code to the client when required.

For example, a server can send JavaScript code that a browser executes.

This constraint is optional in REST.

---

## 9. REST Resources and Endpoints

### Resource

A resource is any identifiable piece of information that an API exposes.

Examples:
- Employee
- Student
- Product
- Order
- Customer
- Payment

In REST, resources are generally identified using URLs.

### Endpoint

An endpoint is a specific URL through which a client interacts with an API.

Example:

| Endpoint | Purpose |
|---|---|
| `/employees` | Access all employees |
| `/employees/101` | Access employee with ID 101 |
| `/departments` | Access all departments |
| `/employees/101/salary` | Access employee salary |

**Important:** A resource represents the data or entity, whereas an endpoint is the URL used to access or manipulate it.

---

## 10. JSON and Java Object Mapping

### Serialization

Serialization means converting a Java object into JSON.

Example:

Java Object:

```java
Employee employee = new Employee(101, "John", 50000);
```

JSON:

```json
{
    "id": 101,
    "name": "John",
    "salary": 50000
}
```

### Deserialization

Deserialization means converting JSON into a Java object.

Example:

JSON:

```json
{
    "id": 101,
    "name": "John",
    "salary": 50000
}
```

Java Object:

```java
Employee employee = new Employee(101, "John", 50000);
```

### Jackson

Jackson is a popular Java library used for JSON serialization and deserialization.

Spring Boot's `spring-boot-starter-web` includes Jackson by default in the usual configuration.

Its important class is:

```java
ObjectMapper
```

### ObjectMapper Example

```java
import com.fasterxml.jackson.databind.ObjectMapper;

public class Main {

    public static void main(String[] args) throws Exception {

        ObjectMapper objectMapper = new ObjectMapper();

        Employee employee = new Employee(101, "John", 50000);

        // Serialization: Java Object to JSON
        String json = objectMapper.writeValueAsString(employee);

        System.out.println(json);

        // Deserialization: JSON to Java Object
        Employee emp = objectMapper.readValue(json, Employee.class);

        System.out.println(emp.getName());
    }
}
```

---