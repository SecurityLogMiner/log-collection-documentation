# Product Requirements README

## Table of Contents

1. [Problem Statement](#problem-statement)
2. [Goals and Objectives](#goals-and-objectives)
3. [User Type and Scenarios](#user-personas-and-scenarios)
4. [Functional Requirements](#functional-requirements)
5. [Non-functional Requirements](#non-functional-requirements)
6. [Visual Representations](#visual-representations)
7. [User Experience and Usability Plan](#user-experience-and-usability-plan)
8. [Technical Architecture and Choices](#technical-architecture-and-choices)
9. [Timeline](#timeline)
10. [Dependencies and Bottlenecks](#dependencies-and-bottlenecks)
11. [Testing and Quality Assurance](#testing-and-quality-assurance)
13. [User Documentation and Support](#user-documentation-and-support)
14. [Versioning](#versioning)
15. [Feasibility](#feasibility)
16. [Innovative Features](#innovative-features)
17. [Stakeholder Alignment](#stakeholder-alignment)
18. [Change Management](#change-management)
19. [Evaluation](#evaluation)

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

1. **Data Collection:**
    - The system should be able to collect data from the specified source.
    - Specify supported data formats for efficient data parsing.

2. **Data Processing and Serialization:**
    - The collected data should be processed and serialized for transmission over the TCP connection.

3. **Error Handling and Reliability:**
    - Implement error detection and correction mechanisms.
    - Implement system monitoring and alerting to reduce downtime during system degradation

4. **Destination Data Reception:**
    - Develop a system of database I/O.
    - Create a procedure to integrate with ElasticSearch.
      
5. **User Authentication:**
    - Users permissions are handled with principles of least priveleges
    - Granular permissions using AWS IAM

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
    - 24/7 availability, except during scheduled maintenance periods
6. **Installability (server/client components)**
    - Easy to perform, fast, and well explained through documentation 

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Visual Representations

![](log-collection-visual.png "Log Collection System")

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## User Experience and Usability Plan

The user will need to create an AWs account to access the client.
The credentials will be handled by the AWS Identity and Access Management systems

When they have successfully authenticated, full visibility of log data will be 
available. The user will be able to interact with each log source, download their
data from the central server, and add/remove log sources.

We will make every attempt to ensure compatibility with users with disabilities
as the project progresses.

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Technical Architecture and Choices

The service running on the client machine will be written in Rust.

The reason for Rust being its ability to write and compile to multiple 
operating systems and handle threading and async operations. Along with its 
platform versatility, Rust's *cargo* command line tool has options for testing 
and documentation generation.

The service running on the client machine will be written in Rust. Rust is chosen because it can write and compile to multiple operating systems and handle threading and async operations. Along with its platform versatility, Rust's cargo command-line tool has options for testing and documentation generation. The service running on the server will be a mix of languages, such as Terraform, shell, and Rust. AWS DynamoDB is a NoSQL database to store logs on a centralized server.



<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Timeline

An MVP of this service should be up and running at month 3. This will give 4
months for user testing/additional development.

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---


<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Testing and Quality Assurance

Between now and the 7th month, code and methods will be tested on a regular basis
as outlined in the SDP document [PROVIDE LINK TO SDP README].

### Test Conditions to be met:



#### Client Repo:
1. Command line and Graphical User Interface to configure:
    - the destination address
    - path(s) to log source(s)

#### Documentation Repo:
1. Provides setup instructions for:
    - account management
    - client-deployment
3. Continuous Documentation Deployment here: https://securitylogminer-doc-repo.readthedocs.io/en/latest/

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## User Documentation and Support
User documentation will be written to satisfy the requirements of the 
[documentation requirement section](#documentation-repo)

Support for this project will come as new maintainers are added to the
organization. Since this is an open-source project, forks will be possible under
the allowed [license](PROVIDE LINK TO SOFTWARE LICENSE).

Documentation is setup and hosted on Read The Docs. This type of integration allows for continuous updates to the documentation, whenever a development change occurs. Whenever updates are pushed to our documentation repository on GitHub, Read the Docs automatically rebuilds the documentation, ensuring that users always have access to the most current information. 

Linked documentation: https://securitylogminer-doc-repo.readthedocs.io/en/latest/

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Versioning

- **Major**: breaking changes
- **Minor**: new features
- **Patch**: bug fixes

Stable versions will be available on the Minor versions due to feature
availability.

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Feasibility

The initial team tasked with this project is capable but we recognize that this
will be a considerable amount of work. A minimal viable product is not past
realistic expectations.

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Innovative Features

There are no features that exist within this project that do not exist elsewhere.
What makes this product stand out is its availability on platforms. The service it
provides could pave the way for innovative services due the product's core data
collection service.

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Stakeholder Alignment

Stakeholder approves of overall project vision. 

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Change Management

Updates to software will be accompanied by a 
[Changelog](SUPPLY LINK TO CHANGELOG).

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

---

## Evaluation

The success of this product will be determined by satisfying the defined 
[testing conditions](#testing-and-quality-assurance).

<a href="#table-of-contents" style="font-size: smaller;">back to top</a>

