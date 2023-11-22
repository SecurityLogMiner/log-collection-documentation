# Product Requirements README

## Table of Contents

1. [Problem Statement](#problem-statement)
2. [Goals and Objectives](#goals-and-objectives)
3. [User Personas and Scenarios](#user-personas-and-scenarios)
4. [Functional Requirements](#functional-requirements)
5. [Non-functional Aspects](#non-functional-requirements)
6. [Visual Representations](#visual-representations)
7. [User Experience and Usability Plan](#user-experience-and-usability-plan)
8. [Technical Architecture](#technical-architecture)
9. [Technology Choices](#technology-choices)
10. [Timeline](#timeline)
11. [Dependencies and Bottlenecks](#dependencies-and-bottlenecks)
12. [Testing Plan](#testing-plan)
13. [Quality Assurance](#quality-assurance)
14. [User Documentation and Support](#user-documentation-and-support)
15. [Ongoing Support and Updates](#ongoing-support-and-updates)
16. [Feasibility](#feasibility)
17. [Innovative Features](#innovative-features)
18. [Stakeholder Alignment](#stakeholder-alignment)
19. [Change Management](#change-management)
20. [Evaluation](#evaluation)

---

## Problem Statement

Gathering data from arbitrary log sources should not be a time-consuming task.
Blueteams, network admins, and anyone wanting to record and store the events 
of a service should have an efficient, secure method of doing so.

---

## Goals and Objectives

A stream of log events, provided by the client endpoint, will be packaged and
transported to a central cloud server for storage and retrieval. 

Whether on a windows or \*Nix-based endpoint, a user will be able to create an
account, receive proper credentials, and establish a secure connection between
the source of their logs and the central data-storage server.

Compatibility with ElasticSearch should be available to the user that will
complement the service the central storage server provides.


<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## User Type and Scenarios
| **User**           | **Scenario** | **Priority** |
|--------------------|--------------|--------------|
| *Security Analyst* | As a security analyst, I want to be able to specify relevant log sources for my investigations. |  High   |
| *IT Adminstrator*  | As an IT admin, I want an intuitive interface for configuring, initializing, and retrieving log data. | High | 
| *Network Administrator* | As a Network admin, I want the retrieval of network-related logs to be supported for network analysis. | High |


<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Functional Requirements

Sure, here's a list of five functional requirements for collecting and transporting data from a source to a destination over TCP (Transmission Control Protocol):

1. **Data Collection:**
   - The system should be able to collect data from the specified source.
   - *Requirements:*
     - Define a mechanism to connect to the data source securely.
     - Specify supported data formats for efficient data parsing.

2. **TLS Connection Establishment:**
   - The system should establish a TLS connection with the destination to ensure secure and ordered data transmission.
   - *Requirements:*
     - Implement TLS over TCP socket creation and management.
     - Create, Update, and Revoke certificates with an in-house CA manager

3. **Data Packaging and Serialization:**
   - The collected data should be packaged and serialized for transmission over the TCP connection.
   - *Requirements:*
     - Implement serialization and deserialization mechanisms for efficient data transfer.

4. **Error Handling and Reliability:**
   - The system should handle errors gracefully and ensure reliable delivery of data even in the presence of network issues or packet loss.
   - *Requirements:*
     - Implement error detection and correction mechanisms.
     - Specify procedures for retransmission of lost or corrupted data.
     - Implement system monitoring and alerting to reduce downtime during system degredation

5. **Destination Data Reception:**
   - The destination should be capable of receiving, processing, and storing the transmitted data.
   - *Requirements:*
     - Develop a data storage service.
     - Create a procedure to integrate with ElasticSearch.

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Non-functional Requirements
1. **Latency**
    - Response times should be less than 300ms
    - Support a 50% increase in log traffic
2. **Recovery**
    - Failure recovery without data loss
3. **Compatibility and Compliance**
    - WCAG compliant
    - Data protection compliant
    - Device and system agnostic (windows/\*nix)
4. **Documentation**
    - User and developer documentation
5. **Availability and Maintenance**
    - 24/7 avaiability, except during scheduled maintenance periods

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Visual Representations

![](log-collection-visual "Log Collection System")

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## User Experience and Usability Plan


<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Technical Architecture


<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Technology Choices


<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Timeline


<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---


## Dependencies and Bottlenecks


<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Testing Plan


<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Quality Assurance


<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## User Documentation and Support


<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Ongoing Support and Updates


<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Feasibility


<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Innovative Features


<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Stakeholder Alignment

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Change Management

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Evaluation

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

