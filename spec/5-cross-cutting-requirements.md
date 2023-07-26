---
description: >-
  This section will highlight important requirements or describe any additional
  cross-cutting requirements that apply to this Building Block.
---

# 5 Cross-Cutting Requirements

The cross-cutting requirements described in this section are an extension of the cross-cutting requirements defined in the [architecture specification document](https://govstack.gitbook.io/specification/v/1.0/architecture-and-nonfunctional-requirements). Any implementation MUST adhere to all requirements from [GovStack Security Requirements](https://govstack.gitbook.io/specification/v/1.0/security-requirements).

## 5.1 Use de-normalized databases (REQUIRED)

There are two main reasons for using denormalized databases instead of traditional normalized databases. First, to significantly improve the performance of read queries. This is highly important as databases of the Messaging Building Block will be under a heavy load of requests that in many cases are expected to respond near real-time. Second, to be able to export the content of databases in the format of time-series databases (see below for its reasons). To achieve this, using "UPDATE" and "DELETE" queries in SQL commands SHOULD be disabled. If not, they MUST be avoided by developers and caught by automated tests if still used.

## **5.2 Archive Content of production-level databases continuously (RECOMMENDED)**

By having this capability, it is possible to delete the content of processed data from production-level server databases right after they have been securely archived. This is important to reduce the impact of potential data breaches by security incidents of potentially N number of application servers hosted by different parties.

## **5.3 Time-series databases should be convertible to ready-to-use relational databases and vice versa (RECOMMENDED)**

If done so, using archived datasets, either fully or partially, allows to recover and/or re-engineer lost databases (or just datasets of interest) automatically and in a matter of seconds if such pipelines have been predefined. Also, by converting the content of relational databases into a format of time-series databases, these purely text-based datasets are easily usable by different kinds of databases, analytics tools, etc., not just by the relational database used at first.

## **5.4 Implement using stateless and horizontally scalable components (REQUIRED)**

Technical components (with the exception of relational databases) must be stateless in the sense of the [Service statelessness principle](https://en.wikipedia.org/wiki/Service\_statelessness\_principle).

## **5.5 Implement horizontally scalable Databases (RECOMMENDED)**

At least on the level of active-passive nodes based on the principle of "eventually consistent". **Pending:** initial state for all messages waiting to be queued.

**Queued:** messages that are in the queue to be sent.

**Sent:** messages with proper confirmation that was sent to the provider.

**Delivered:** messages with proper confirmation that was delivered to the end-user.

**Errored:** messages with an error during delivery.

**Failed:** messages that are errored and we gave up sending.

## **5.6 Messaging as a service must be vendor-neutral (REQUIRED)**

If Messaging Building Block protocols are followed, the technical stack used to provide messaging as a service is vendor-neutral, meaning that anyone is free to use technical solutions of their own choice.

## **5.7** Only allowed participants can join the network (REQUIRED)

Only allowed participants are allowed to provide and use the services of Messaging Building Block.

## 5.8 Do not store users' contacts and readable messages at Messaging Building Block (REQUIRED)

Messaging Building Block is a dumb messaging proxy that gets all of its relevant input from its clients. This also includes the names and contact information of all relevant participants. Such sensitive information may not exist in its raw and/or re-engineerable form nor in databases or logs.

## **5.9 Message content must be readable only by intended participants (REQUIRED)**

Depending on the specific use case, this may mean [end-to-end encryption](https://en.wikipedia.org/wiki/End-to-end\_encryption) or [SNI routing](https://en.wikipedia.org/wiki/Server\_Name\_Indication).

## **5.10 Audit logs must be provided (REQUIRED)**

Every instance of a service must generate audit logs containing information about all of its actions regarding timestamps, related parties, identifiers to operations performed, and HTTP response codes for any given action. Audit logs may not contain the actual content of the message. Audit logs must be in a time series database format. Audit logs must be accessible by a given endpoint by the central service provider only. Audit logs should be periodically removed from their original source after a defined period of time.

## **5.11** Secure API exposure **(REQUIRED)**

All APIs are exposed via secure socket connections (HTTPS).

## **5.12 A**ccess quotas **(RECOMMENDED)**

Manage access quotas and throttling.

## **5.13 API calls** **(REQUIRED)**

Logging of all API calls made.

## **5.14 API consumption (RECOMMENDED)**

Allow API providers to limit the rate of consumption for all API users.

## **5.15 S**tandardized backend error messages **(REQUIRED)**

Transform backend error messages into standardized messages so that all error messages look similar; this also eliminates exposing the backend code structure.

## **5.16** Minimal data for requests **(REQUIRED)**

Contact address (email, phone number, etc.), the message type, the content of the message, and the initiating source’s unique transaction ID.

## **5.17** Messaging processing **(REQUIRED)**

Asynchronous messaging processing. OpenAPI specifications for calling this function; resource models and data structures, internal and external interfaces.

## **5.18** Stateless architecture **(REQUIRED)**

Stateless architecture.

## **5.19** Message broker tool **(RECOMMENDED)**

Message broker tool to enable performant queueing mechanisms such as RabbitMQApache/Kafka, or GRPC for data transfer speed purposes.

## **5.20 U**nstructured DATABASES **(REQUIRED)**

Databases with unstructured data should be treated with Elasticsearch/Logstash.

## **5.21** Message broker tool **(RECOMMENDED)**

End users should be registered as Message queue clients/subscribers in the Messaging Building Block. Subscription is required to receive a message.
