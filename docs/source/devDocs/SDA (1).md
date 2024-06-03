# Software Design and Architecture README

## Table of Contents

1. [Introduction](#introduction)
2. [Architectural Goals and Principles](#architectural-goals-and-principles)
3. [System Overview](#system-overview)
4. [Architectural Patterns](#architectural-patterns)
5. [Component Descriptions](#component-descriptions)
6. [Client Component](#client-component)
7. [Documentation Component](#documentation-component)8
8. [Data Management](#data-managament)
9. [Client Data](#client-data)
10. [Server Data](#server-data)
11. [Interface Design](#interface-design)
12. [Considerations](#considerations)
13. [Security](#security)
14. [Performance](#performance)
15. [Maintenance and Support](#maintenance-and-support)
16. [Deployment Strategy](#deployment-strategy)
17. [Testing Strategy](#testing-strategy)
18. [Glossary](#glossary)

---

## Introduction
This document provides a comprehensive guide to the development methodology, outlining activities, goals, roles, tools, testing procedures, timelines, risk management, documentation practices, and continuous improvement strategies.


The log collection service should take an event log, process each event 
line, and send the data to a central server. The priority is the confidentiality, 
integrity, and availability of all data flowing through this service pipeline.

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Architectural Goals and Principles
The main architectural goals and principles are security, scalability, 
abstraction, and modularity. Architectural principles include maintaining proper 
software security practices, designing modular systems, and performing 
comprehensive tests to prove functionality.

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## System Overview
An open-source tool that is available to users. The application will function on 
various operating systems, which will be tested through deployment on VMS.
The centralized server is expected to run on a Linux server to receive all the 
event logs sent by user endpoints. AWS will deploy the server.

Starting at the Data Source, event lines are sent to the Data Processing and 
Monitoring module, where they are serialized and staged to be sent across the 
network.

![](log-collection-visual.png "Log Collection System")
<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---


## Architectural Pattern
We will adapt the client-server, producer consumer pattern, and event sourcing pattern.

### Client Server Pattern
The client-server model, where the clients on endpoints send event logs to a 
centralized server for processing and storage.

### Producer Consumer Pattern
Any component that needs to handle the input -> output of data asyncronously will
benefit from using threads to break up tasks for efficiency of time and/or
memory.

### Event Sourcing Pattern
For flexible, real-time data handling, this pattern can be beneficial to stream 
and store log data continuously.

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Component Descriptions


### Web Front-End Component
The web frontend will provide the documentation and act as the public landing page for the project.

The web frontend will also house the user documentation. See (documentation)[#documentation-component] section.


### Client Component
The client will have full visibility of log data. The user will be able to interact with each log source, download log 
data from the central server, and add/remove log sources.

From either the GUI or command-line interface, the user will provide
configuration file that contains a path (or paths) to the log sources, the format
of the log for each of the supplied paths and the table name on AWS.

[Client Repository](https://github.com/SecurityLogMiner/log-collection-client)


### Documentation Component
It does not have to be complicated but it must be organized. Projects die when
the documentation is either unavailable or lacks enough information to help users
(and developers) get started.

At a minimum, the user documentation should include the following:
1. Getting Started:
    - how to create an account
    - how to install software
    - how to run the client
    - configuration guidelines


Developer and User documentation will be hosted on ReadTheDocs.
[Doc Project Link](https://securitylogminer-doc-repo.readthedocs.io/en/latest/)

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Data Management


### Client Data
Incoming log data will be defined using the configuration file located on the client. The current format is:
```
[[dynamodb.package]]
source = "./logs/test1.log"
table = "SecurityLog1"
```


### Server Data
Each user will require an isolated database instance and each log source will be
stored in a corresponding table. 


<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Interface Design

The interface design will consists of event logs coming from a primary source such as an endpoint. This data will be showcased and alerted and notify the system whether the log 
information contains malicious content.

The majority of the details provided will be encapsulated by the <a href="#component-descriptions" style="font-size: smaller;">component descriptions.</a>
The interface will consist of a front-end implementation using Svelte and Rust for the backend functionality.

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Considerations

### Security
Focus on: Confidentiality, Integrity, Availability

The server will generate the client's public and private key. This private key will be generated through AWS. The client's private key should not be hardcoded, it is read in from the terraform script. If the user deletes their account, their information should be removed from all databases and tables The server will use role-based access control to ensure users can only perform the actions that they are authorized for. TLS will ensure encrypted data transmission. 

---

### Performance
Long-term goal is that the server is able to scale the database instances for all
users using the service. 

While system dependent, the client should be able to handle around 5K events per 
second. Read the following for Event-Per-Second:


[Event Per Second](https://content.solarwinds.com/creative/pdf/Whitepapers/estimating_log_generation_white_paper.pdf)

Performance Testing: Conduct performance testing to identify bottlenecks and optimize critical parts of the system.

Monitoring: Implement performance monitoring to track resource utilization, response times, and system health.

Load Balancing: Implement load balancing to distribute traffic evenly across multiple system instances.

### Maintenance and Support
Members of the organization are able to help maintain the project, with a
handful of CODEOWNERS that help guide the updates as the project grows.

Anyone using the product will be able to submit issues that will be used to

make improvements and take suggestions under consideration.

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

# Testing Strategy
Using Postman and Rust tests, testing can be accomplished at any step in the
software development stage. First, for each feature, the contributor will:

    1. Analyze the requirements
    2. Plan appropriate tests (security, performance, regression, user)
    3. Execute those tests
    4. Use the results of the test for further discussion

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Glossary

| **Terminology**           | **Definition** |
|--------------------|--------------|
| *User Interface* |  User interactions are managed by a front-end implementation.|
| *Backend Server*  |  Processes requests, business logic, and interfaces with the database. |
| *Database* |Stores and manages data within a database for event logs in AWS. |
| *Data Producer* | Grabs a raw line from the event log |
| *Data Consumer* | Parses raw line using config format |
| *Collector* | Formatted and Serialized data is queued for Sender |
| *Sender* | Depending on central server status, the data is sent to its location|
| *Listeners* | Listen for status |
| *API* | Application Programming Interface: provides an interface for working with their specified components|
| *Central Server*| The destination of formatted event logs |
| *Offline Storage* | Data reservoir for redundancy/recovery if needed.|
| *AWS* | Centralized Server using Amazon Web Services|
| *Endpoint* | Device of a system that sends or receives data|
| *CRUD* | Create, Read, Update and Delete|
| *SSL\TLS* | Secure Sockets Layer or Transport Layer Security are protocols for encrypting data transmitted over the web. Ensures secure communication between a client and server|
|*Event Logs*| Records events or activities generated by a system or network|
|*Centralized Server*| Single server to collect and manage services from multiple endpoints|
|*TOTP*| Time based one-time password in RFC 6238|


<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---


