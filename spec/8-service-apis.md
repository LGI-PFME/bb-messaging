---
description: >-
  This section provides a reference for APIs that should be implemented by this
  Building Block.
---

# 8 Service APIs

This section provides a reference for APIs that should be implemented by this Building Block. The APIs defined here establish a blueprint for how the Building Block will interact with other Building Blocks. Additional APIs may be implemented by the Building Block, but the listed APIs define a minimal set of functionality that should be provided by any implementation of this Building Block.

The [GovStack non-functional requirements document](https://govstack.gitbook.io/specification/v/1.0/architecture-and-nonfunctional-requirements/6-onboarding) provides additional information on how 'adaptors' may be used to translate an existing API to the patterns described here. This section also provides guidance on how candidate products are tested and how GovStack validates a product's API against the API specifications defined here.&#x20;

The tests for the Scheduler Building Block can be found in [this GitHub repository.](https://github.com/GovStackWorkingGroup/bb-messaging/tree/main/test/openAPI)

## 8.1 Government to person (G2P)

### 8.1.1 Sending emails

### 8.1.1.1 Sending single emails one by one

This API is designed to send out emails one by one.

Although an email can be sent to multiple recipients by using `email`, `emailCC` and `emailBCC` appropriately, this is still considered as sending a single email.

#### Sample user story

As a Doctor working in a hospital, I want to notify my patient about a confirmed registration so that the patient would know when to come for a visit.

#### API endpoint

{% swagger src="https://raw.githubusercontent.com/GovStackWorkingGroup/bb-messaging/main/api/swagger.yaml" path="/send/email/single" method="post" %}
[https://raw.githubusercontent.com/GovStackWorkingGroup/bb-messaging/main/api/swagger.yaml](https://raw.githubusercontent.com/GovStackWorkingGroup/bb-messaging/main/api/swagger.yaml)
{% endswagger %}

### 8.1.1.2 Sending multiple (batch) emails at once

This API is designed to send out identical emails to multiple (batch) recipients at once.

#### Sample user story

As a Hospital I want to notify a specified group of my clients about the possibility to register to vacant time slots within a limited period of time so that the clients potentially needing it the most would have a guaranteed chance to get an appointment

#### API endpoint

{% swagger src="https://raw.githubusercontent.com/GovStackWorkingGroup/bb-messaging/main/api/swagger.yaml" path="/send/email/batch" method="post" %}
[https://raw.githubusercontent.com/GovStackWorkingGroup/bb-messaging/main/api/swagger.yaml](https://raw.githubusercontent.com/GovStackWorkingGroup/bb-messaging/main/api/swagger.yaml)
{% endswagger %}

## 8.2 Person to Government (P2G) <a href="#docs-internal-guid-c38a9447-7fff-fcb5-e6eb-c6419072f004" id="docs-internal-guid-c38a9447-7fff-fcb5-e6eb-c6419072f004"></a>

### 8.2.1 Responding to emails

This API is designed to accept responses to emails that have been previously sent out by using the Messaging Building Block. The protocol itself is lightweight and expects custom services from anyone using it. The Messaging Building Block is responsible for delivering the message and does not know (or want to know) anything about the content of it, how it will be used, etc.

#### Sample user story

As a Hospital, I want to get and send responses from and to clients so that I could continue and keep track of email conversations taking place via GovStack

#### API endpoint

{% swagger src="https://raw.githubusercontent.com/GovStackWorkingGroup/bb-messaging/main/api/swagger.yaml" path="/callback/email" method="post" %}
[https://raw.githubusercontent.com/GovStackWorkingGroup/bb-messaging/main/api/swagger.yaml](https://raw.githubusercontent.com/GovStackWorkingGroup/bb-messaging/main/api/swagger.yaml)
{% endswagger %}

### 8.2.2 Reading the status of emails

This API is designed to provide information about the status of emails sent to the Messaging Building Block.

#### Sample user story

As a Doctor working in a hospital I want to know which emails I have sent haven't reached their destination so that I could contact such patients by using different means

#### API endpoint

{% swagger src="https://raw.githubusercontent.com/GovStackWorkingGroup/bb-messaging/main/api/swagger.yaml" path="/status/email" method="get" %}
[https://raw.githubusercontent.com/GovStackWorkingGroup/bb-messaging/main/api/swagger.yaml](https://raw.githubusercontent.com/GovStackWorkingGroup/bb-messaging/main/api/swagger.yaml)
{% endswagger %}

#### Status of emails

Possible status of emails that can be queried are as follows:

1. `scheduled`
2. `processing`
3. `deferred`
4. `bounced`
5. `not sent`
6. `delivered`

There is no keeping track of emails which have been sent successfully, as this would end up creating and maintaining a massive database of emails, their senders and recipients, etc., which would be wrong for so many reasons.
