---
description: >-
  This section will highlight important requirements or describe any additional
  cross-cutting requirements that apply to this Building Block.
---

# 5 Cross-Cutting Requirements

The Cross-cutting requirements described in this section are an extension of the cross-cutting requirements defined in the architecture specification document. This section will describe any additional cross-cutting requirements that apply to this Building Block.

Cross-cutting requirements will use the same language (MUST or SHOULD) as specified in the architecture document.

## 5.1 Denormalized databases MUST be used

There are two main reasons for using denormalized databases instead of traditional normalized databases.

First, to significantly improve the performance of read queries. This is highly important as databases of the Messaging Building Block will be under a heavy load of requests that in many cases are expected to respond near real-time.

Second, to be able to export the content of databases in the format of time-series databases (see below for its reasons).

To achieve this, using "UPDATE" and "DELETE" queries in SQL commands SHOULD be disabled. If not, they MUST be avoided by developers and caught by automated tests if still used.

## **5.2 Content of production-level databases SHOULD be continuously archived centrally**&#x20;

By having this capability, it´s possible to delete the content of processed data from production-level server databases right after they have been securely archived.

This is important to reduce the impact of potential data breaches by security incidents of potentially N number of application servers hosted by different parties.

## **5.3 Time-series databases SHOULD be convertible to ready-to-use relational databases and vice versa**

If done so, using archived datasets, either fully or partially, allows to recover and/or re-engineer lost databases (or just datasets of interest) automatically and in a matter of seconds if such pipelines have been predefined.

Also, by converting the content of relational databases into a format of time-series databases, these purely text-based datasets are easily usable by different kinds of databases, analytics tools, etc., not just by the relational database used at first.

## **5.4 SHOULD enable message replication**

In order to prevent single points of failure, messages must be replicated on at least 2 different service providers.

In case of message replication, all unprocessed replicated messages MUST be kept track of and relevantly updated in order to prevent re-processing them.

## **5.5 MUST support policy configuration**

Admin of the room must be able to choose the policy profile with the configuration of the message provider, e.g. retrial frequency.

## **5.6** MUST support queuing mechanism

Unsent and unsuccessfully delivered messages must remain in a queue until being successfully delivered or otherwise permanently processed.

### **Messages Delivery Statuses**

**Pending:** initial state for all messages waiting to be queued.

**Queued:** messages that are in the queue to be sent.

**Sent:** messages with proper confirmation that was sent to the provider.

**Delivered:** messages with proper confirmation that was delivered to the end-user.

**Errored:** messages with an error during delivery.

**Failed:** messages that are errored and we gave up sending.

### Delivery business rules

**Messages not delivered in a period of 24 hours:** Any errored or queued messages more than 24 hours old must be labeled as failed and be removed from the queue.

**Messages retrial:** Errored messages must be retried for 24 hours.

## 5.7 All published software updates MUST produce a new version number&#x20;

Software update versioning follows the concept of [Semantic Versioning](https://semver.org/).

## 5.8 MUST be backward compatible in case of updates within the same major release

When adding new functionalities and/or messaging platforms, previous developments must remain intact if not deliberately changed or removed.

## 5.9 MUST follow OpenAPI annotations

A protocol describing the technical usage of any given or planned messaging types/platforms is mandatory.

The source code of applications must be covered with OpenAPI annotations.

Deployment of an application produces an updated version of the publicly accessible Swagger User Interface in case the technical specification has changed.

## **5.10 MUST use test-driven development**

All technical functionalities must be fully covered by automated tests.

## **5.11 All technical components MUST be stateless and horizontally scalable**

Technical components (with the exception of relational databases) must be stateless in the sense of the [Service statelessness principle](https://en.wikipedia.org/wiki/Service\_statelessness\_principle).

## **5.12 Databases SHOULD be horizontally scalable**

At least on the level of active-passive nodes based on the principle of [Eventually consistent](https://en.wikipedia.org/wiki/Eventual\_consistency).

## **5.13 Messaging as a service MUST be vendor-neutral**

If Messaging Building Block protocols are followed, the technical stack used to provide messaging as a service, is vendor-neutral, meaning that anyone is free to use technical solutions of their own choice.

## **5.14** Only allowed participants MUST be able to join the network

Only allowed participants are allowed to provide and use the services of Messaging Building Block.

## 5.15 Central databases of users' contacts and readable messages MUST NOT exist at Messaging Building Block

Messaging Building Block is a dumb messaging proxy that gets all of its relevant input from its clients. This also includes the names and contact information of all relevant participants.

Such sensitive information may not exist in its raw and/or re-engineerable form nor in databases or logs.

## **5.16 Message content MUST be readable only by intended participants**

Depending on the specific use case, this may mean

1. [end-to-end encryption](https://en.wikipedia.org/wiki/End-to-end\_encryption); or
2. [SNI routing](https://en.wikipedia.org/wiki/Server\_Name\_Indication).

## **5.17 MUST support audit logging**

Every instance of a service must generate audit logs containing information about all of its actions regarding timestamps, related parties, identifiers to operations performed, and HTTP response codes for any given action.

* Audit logs may not contain the actual content of the message.
* Audit logs must be in a time series database format.
* Audit logs must be accessible by a given endpoint by the central service provider only.
* Audit logs should be periodically removed from their original source after a defined period of time.

## **5.18 Cloud native is a MUST**

All stand-alone applications used and services created based upon them must be cloud-native in the sense of [cloud-native computing](https://en.wikipedia.org/wiki/Cloud-native\_computing).

## **5.19** Source code MUST be published under a permissive license and be easily accessible by a public repository

The full source code of the Building Block must be published as easily accessible open-source code.

All custom developments are published under the MIT License by default if not clearly stated otherwise.

## Security requirements&#x20;

In case of not applying any or some of [GovStack's global cross-cutting security requirements](https://govstack.gitbook.io/specification/v/govstack-specification-main/security-requirements), listing all such cases is a must.

The messaging system must comply with the security requirements on the security [building block](https://docs.google.com/document/d/1ZuR52EJm-iWWXCNpkAEZXFPRF1Cg1ciJ/edit) on:

* **4 Key Security Functional Requirements**
* **5.1 Privacy**
* **5.2 Audit Logging**
* **5.3 Source Code**
* **6.1 API Management and Gateway Functional Requirements**
* **6.2 Identity and Access Management (IAM) Suite Functional Requirements**
* **6.3 Digital ID/Certificate Functional Requirements**
* **6.4 Certificate Authority Functional Requirements**
* **6.8 Virus, Ransomware, Malware, Spam, Phishing Protection Requirements**
* **6.9 Denial of Service Attack Prevention Requirements**
* **6.10 Applications Development Vulnerability Prevention Requirements**
* **6.11 Infrastructure Vulnerability Remediation Requirements**
* **6.13 Data Encryption at Rest and In Transit Requirements**
* **6.14 Social Network, Media, and Engineering Threat Management Requirements**
* **6.21 Fraud Prevention, Detection, and Management Requirements**
