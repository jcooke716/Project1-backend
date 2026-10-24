# Expense Reimbursement API: Javalin and JDBC

A Java backend that brings employee account queries and administrator reimbursement views into one HTTP service.

## Problem and approach

A reimbursement interface needs a shared API for employee information, pending expenses, and resolved records. This project exposes those operations through Javalin routes and keeps database queries behind service and DAO interfaces.

## Implementation

| Layer | Location | Responsibility |
| --- | --- | --- |
| HTTP | [EndPointsMain.java](src/main/java/endpoints/EndPointsMain.java) | Starts Javalin on port 4040 and registers the API routes. |
| Service | [src/main/java/service/](src/main/java/service/) | Coordinates administrator and employee operations. |
| Persistence | [src/main/java/dao/](src/main/java/dao/) | Performs PostgreSQL access through JDBC. |
| Data objects | [src/main/java/pojo/](src/main/java/pojo/) | Represents employees, administrators, pending expenses, and final records. |
| Schema | [DatabaseScript](src/main/resources/DatabaseScript) | Initial database structure. |

The entry point includes administrator lookup and login, employee lookup and profile updates, employee-specific pending and resolved requests, and administrator views across reimbursement records.

## Representative routes

| Method | Path | Purpose |
| --- | --- | --- |
| GET | `/api/v1/employees` | List employees. |
| GET | `/api/v1/employees/{eid}` | Look up an employee for administrator views. |
| GET | `/api/v1/pending/{eid}` | Retrieve an employee's pending expenses. |
| GET | `/api/v1/resolved/{eid}` | Retrieve an employee's resolved expenses. |
| PUT | `/api/v1/update` | Update employee information. |
| GET | `/api/v1/expenses/pending` | Retrieve pending expenses for administrator review. |

See the entry point for the complete route definitions.

## Local preparation

Use a JDK, Maven, and PostgreSQL. Import the Maven project into an IDE, align `src/main/java/dao/DButil.java` with the local database, and review the schema draft before initializing tables. The JDBC database name and schema's database declaration are not currently aligned.

Launch `endpoints.EndPointsMain` after configuring the compiler and database. The service listens on port 4040.

## Portfolio focus and current scope

HTTP API organization, layered Java design, JSON handling, and relational persistence. This version concentrates on the combined API rather than container delivery or Spring Data JPA. Some service and DAO methods remain incomplete, so the listed code paths should not be treated as a verified end-to-end deployment or a production authorization system.
