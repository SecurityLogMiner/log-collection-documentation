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
Architectural principles include Maintaining proper software security practices, designing systems into hierarchies, striving for feature flexibility, and performing capable tests to ensure good performance.


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

### Performance

### Maintenance and Support

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Testing Strategy

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Glossary

| **Term**           | **Scenario** |
|--------------------|--------------|
| *User Interface* |  User interactions and managed by a front end implementation.|
| *Backend Server*  |  Processes requests, business logic, and interfaces with the database. |
| *Database* |Stores and manages data within a database for event logs in AWS. |
<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---


