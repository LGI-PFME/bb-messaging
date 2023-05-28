---
description: This section lists the technical capabilities of this Building Block.
---

# 6 Functional Requirements

This section lists the technical capabilities of the Messaging Building Block. The following components are needed to achieve the technical functionalities of the messaging Building Block.

<figure><img src=".gitbook/assets/image3 (1) (1).png" alt=""><figcaption><p><a href="https://app.diagrams.net/?src=about#G1AD6Ez1Q68ED1xB1JCpTuVshKYWp8VGvK">https://app.diagrams.net/?src=about#G1AD6Ez1Q68ED1xB1JCpTuVshKYWp8VGvK</a></p></figcaption></figure>

### 6.1 Messaging request initiation

Handles the initiation of input data processing from all the API messaging calls and makes the API access control verification from other Building Blocks to the Messaging Building Block and vice versa as well as within the Messaging Building Block, it will:

* use Identity and access management for authentication;
* perform input validation checks to prevent oversized message attacks, SQL injection attacks as well as JSON and XML threats;
* require authentication for all API users;
* manage access quotas and throttling;
* logging of all API calls made;
* allow API providers to limit the rate of consumption for all API users;
* transform backend error messages into standardized messages so that all error messages look similar (this also eliminates exposing the backend code structure).

&#x20;This request could come from two sources: external or internal. An external source could be another GovStack Building Block (e.g. the Registration Building Block). Either source must be appropriately authenticated and authorized to initiate the request. The request must contain at a minimum: the contact address (email, phone number, etc.), the message type, the content of the message, and the initiating source’s unique transaction ID.

### **6.2 Queuing**

The queuing process varies according to the policy and message type attached to the messaging, if an emergency messaging type applies to it, the messaging gets prioritized, otherwise, the FIFO algorithm (First In, First Out) applies to other message types. It saves all the requests for further processing, furthermore, works in the form of an "AS IS" process analysis without changing anything on the request. The message queueing mechanism will:

* save a hash (MHASH) of the original request and a Unique Message ID (UMID);
* respond with "Message received" to the sender with generated UMID.

### **6.3 Validation and Verification**

Messaging requests go through a final check to be clean of defects and inconsistencies, to check with external systems as necessary:

* check for message duplicates by making an actual request to a Time Series Database to see if entries with MHASH and UMID exist;
* low-level validation of data types and data completeness;
* check for inconsistencies;
* standard error messages and codes are used as a response to inconsistent requests.

### **6.4 Workflow and Scheduling**

* In relation to batch logic, messages are scheduled against the availability of systems, throughput limitations, and rules set by programs.
* Regular and repeat messages are scheduled.
* Batches may be given prioritization in the queue according to the message settings.
* The essential control logic may be included here specific to the individual batch sending and resending.
* Additional workflow checks as required, including resending failed transactions.

### **6.5 Batch logic**

* Find unprocessed requests from a database.
* Prepare each request for actual processing, requests may come as single or batch messages and every message needs to be treated as a separate entry.
* It prepares unprocessed requests for actual processing.

### **6.6 Audit trails**

Each component of the messaging building block should be capable of producing transaction logs.  This is important to ensure that the system can be adequately monitored and troubleshooting can be performed efficiently and effectively.

The components should also generate transaction logs for events that capture at least the following information:

* transaction date and time;
* transaction source;
* transaction destination;
* supplementary data;
* transaction status (success, failed, in progress).

The event logs and the transaction logs should **NOT** capture any sensitive data such as contact data, or channel authorization credentials.

Fetch and securely archive logs from working nodes is also expected.

### **6.7 Security layer**

The security layer ensures that the content of messages and interactions with other Building Blocks are encrypted in transit. The security layer follows these requirements:

* The communication must be TLS-secured using client authentication, Transport Layer Security protocol (TLS) 1.2 and above should be used to protect the confidentiality and integrity of the data in transit.
* Personal profiles must never be disclosed to any unauthorized party.

## Design and Components of Messaging Building Block <a href="#docs-internal-guid-d85f59a4-7fff-1564-6ae2-86d67f36a258" id="docs-internal-guid-d85f59a4-7fff-1564-6ae2-86d67f36a258"></a>

1. The Messaging Building Block is part of the GovStack implementation and is prompted to open up a two-way communication channel to deliver and capture messages/data between the GovStack systems and the end users, physical and legal persons.
2. As a rule, the Messaging Building Block does not own any information but is carrying the minimum amount of (meta) data needed to transfer/publish a message. Messaging Building Block allows other Building Blocks and applications to reach out to customers/citizens in order for them to be able to make a decision or access a service. This Building Block can also be used for broadcasting a disaster message.
3. Messaging policies are configurable modalities and channels that can be accessed/utilized through the Messaging Building Block in order to reach out to the users or groups. This Building Block is using existing applications/channels, such as e-mail, SMS, and messaging platforms for enabling users to subscribe to an application/channel provided by Messaging Building Block itself for text-based content.
4. Having published its messaging policies and services at the Information Mediator Building Block, the other Building Blocks and applications can discover and use the services of the Messaging Building Block.
5. Messaging Building Block allows for asynchronous communication, using either point-to-point communication or a Pub/Sub model (using Information Mediator Building Block) where the user is subscribed to a message room/group and will be receiving all messages intended for the “mother of newborn child” group.
6. Security: Before allowing any messages to be published, the Messaging Building Block fetches a corresponding ID and a role or a session token available for the user for authentication and access purposes. Incorporates privacy into its design when the purpose of the authentication is not revealed if a service provider sends an authentication request.

## **Example Security Requirement**

List any cross-cutting security requirements that apply to the context from [Detailed Functional Requirements](https://www.govstack.global/wp-content/uploads/2021/08/Security\_Building\_Block\_Definition\_1.0.1.pdf).

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

## **Messaging Building Block technical requirements**

<table data-header-hidden><thead><tr><th width="431.5"></th><th></th></tr></thead><tbody><tr><td><strong>Requirement</strong></td><td><strong>Type (Must/Should/May)</strong></td></tr><tr><td>Secure API exposure:  All APIs exposed via secure socket connections (HTTPS).</td><td>Must</td></tr><tr><td>Client application authorisation tokens: Client applications must send authorization tokens in the authorization header of the request to authenticate users and the API Management Gateway will verify whether the token is valid.</td><td>Must</td></tr><tr><td>Perform input validation checks to prevent oversized message attacks, SQL injection attacks as well as JSON and XML threats.</td><td>Must</td></tr><tr><td>Manage access quotas and throttling.</td><td>May</td></tr><tr><td>Logging of all API calls made.</td><td>Must</td></tr><tr><td>Allow API providers to limit the rate of consumption for all API users.</td><td>Should</td></tr><tr><td>Transform backend error messages into standardized messages so that all error messages look similar; this also eliminates exposing the backend code structure.</td><td>Should</td></tr><tr><td>Minimal data for requests: contact address (email, phone number, etc.), the message type, the content of the message, and the initiating source’s unique transaction ID.</td><td>Must</td></tr><tr><td>Asynchronous messaging processing.</td><td>Must</td></tr><tr><td>OpenAPI specifications for calling this function; resource models and data structures, internal and external interfaces.</td><td>Must</td></tr><tr><td>Stateless architecture.</td><td>Must</td></tr><tr><td>Message broker tool to enable performant queueing mechanisms such as RabbitMQ, Apache/Kafka, or GRPC for data transfer speed purposes.</td><td>Should</td></tr><tr><td>Databases with unstructured data should be treated with Elasticsearch/Logstash.</td><td>Must</td></tr><tr><td>End users should be registered as Message queue clients/subscribers in the Messaging Building Block. Subscription is required to receive a message.</td><td>Should</td></tr></tbody></table>
