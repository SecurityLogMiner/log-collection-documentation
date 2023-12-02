# Software Design and Architecture README

## Table of Contents

1. [Introduction](#introduction)
2. [Architectural Goals and Principles](#architectural-goals-and-principles)
3. [System Overview](#system-overview)
4. [Architectural Patterns](#architectural-patterns)
5. [Component Descriptions](#component-descriptions)
6. [Data Management](#data-managament)
7. [Interface Design](#interface-design)
8. [Considerations](#considerations)
9. [Security](#security)
10. [Performance](#performance)
11. [Maintenance and Support](#maintenance-and-support)
13. [Deployment Strategy](#deployment-strategy)
14. [Testing Strategy](#testing-strategy)
15. [Glossary](#glossary)

---

## Introduction

This document will outline the architecture for a command line-based security logger system where blue team members can access security logs from a centralized server. The project will use OS APIs to read log data and send it to a centralized processing and database server. The server will be plugged into an Elastic stack for more efficient visualization and investigative functionality. 

The log collection service should take an event log, process each event line, and send the data to a central server. The priority is the confidentiality, integrity, and availability of all data flowing through this service pipeline.

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Architectural Goals and Principles

The main architectural goals and principles are security, scalability, abstraction, and modularity.
Architectural principles include maintaining proper software security practices, designing systems into hierarchies, striving for feature flexibility, and performing capable tests to ensure good performance.


<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## System Overview

An open-source tool that is available to users. The application will live and function on various platforms and operating systems, which will be tested through deployment on VMS.
The centralized server is expected to run on a Linux server to receive all the event logs sent by machines. AWS will deploy the server.

Starting at the Data Source, event lines are sent to the Data Processing and Monitoring module, where they are serialized and staged to be sent across the network. The internal communication will be managed through sockets while the external communication is handled by WebSockets, allowing for low-latency monitoring and data feeding. 

![](log-collection-visual.png "Log Collection System")
<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Architectural Patterns
We will use event-sourcing, producer/consumer, and some form of layering.

### Client Server Pattern
The client-server model, where the clients on endpoints send security logs to a centralized server for processing and storage. This pattern provides centralized management of log data. We will adapt the client-server model, event-sourcing, and microservices patterns. 

### Microservices Pattern
Break down the centralized processing and database server into microservices, each responsible for a specific aspect of log processing. This can make updates and maintenance easier.

### Pub-sub Pattern
Implement a publish-subscribe system for the central server to distribute log data efficiently. This can help in managing the asynchronicity of log data collection.

### Event Sourcing Pattern:
For real-time data handling, this pattern can be beneficial to stream and store log data continuously. It's flexible for handling real-time data and events.


<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Component Descriptions

### Web Frontend component:
The web frontend will provide the user registration, account login, and distribution 
of the following:
- TLS certificates and their private keys
- ability to copy their OTP data (important because it is not preserved)
- software binary distribution.
- quick glance of existing log sources (not the log data itself)
- The instance IP and port connected to their account

The web frontend will also house the user documentation. See (documentation)[#documentation-component] section.

Repo: (web frontend)[https://github.com/SecurityLogMiner/log-collection-frontend]

### Client component:
The client will consist of a GUI (default) that prompts the user to provide either 
their OTP or user/pass. Once authenticated, the user will have full visibility of 
log data. The user will be able to interact with each log source, download log 
data from the central server, and add/remove log sources.

While the default frontend will be a GUI, the user has the option of running the
software from a command-line interface. 

In either case, the client frontend will use the same functionality to accomplish
the tasks.

From either the GUI or command-line interface, the user will provide
configuration file that contains a path (or paths) to the log sources, the format
of the log for each of the supplied paths, a destination IP/port, and the
certificate and private key information they were supplied from the web
interface.

Repo: (client)[https://github.com/SecurityLogMiner/log-collection-client]

### API component:
This component of the product will handle all the requests from the client, and
on behalf of the client, including:
- account creation/deletion/authentication
- software distribution
- certificate download
- certificate revokation/renewal
- Single OTP issuance 
- user list retrieval (server only)
- instance configuration

These api endpoints must also be protected. The server component must be the only
entity that is allowed to revoke and renew certificates, issue OTPs, and retrieve a
list of existing users.

Each client should be able to access account information by providing api
verification tokens.

Repo: (api)[https://github.com/SecurityLogMiner/log-collection-api]

### Server component:
Considering that the central server will be a destination for many users, it is
important that this component of the project can scale in the future. For now,
during beta testing, the server should be able to create isolated instances for
each user that is generating incoming logs.

Each instance will be tied to a user using a unique key generated an existing, 
(and validated) user. Each instance will store the incoming logs into a database 
instance and provide an extension to ElasticSearch should the user want that 
additional functionality.

Repo: (server)[https://github.com/SecurityLogMiner/log-collection-server]

### Documentation component:
It does not have to be complicated but it must be organized. Projects die when
the documentation is either unavailable or lacks enough information to help users
(and developers) get started.

At a minimum, the user documentation should include the following:
1. Getting Started:
    - how to create an account
    - how to install software
    - how to run the client
    - configuration guidelines

2. Dashboard Information:
    - layout
    - how to view logs

3. What else?

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Data Management

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Interface Design

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Considerations


### Security
Focus on: Confidentiality, Integrity, Availability

### Performance

### Maintenance and Support

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

# Testing Strategy

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
|*Event Logs*| Rercods events or activities generated by a system|
|*Centralized Server*| Single server to collect and manage services from multiple endpoints|


<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---


