---
description: >-
  This section provides a reference for APIs that should be implemented by this
  Building Block.
---

# 8 Service APIs

This section provides a reference for APIs that should be implemented by this Building Block. The APIs defined here establish a blueprint for how the Building Block will interact with other Building Blocks. Additional APIs may be implemented by the Building Block, but the listed APIs define a minimal set of functionality that should be provided by any implementation of this Building Block.

[Messaging Building Blocks' APIs](https://github.com/GovStackWorkingGroup/bb-messaging/tree/1.0-QA/api).

The [GovStack non-functional requirements document](https://govstack.gitbook.io/specification/v/1.0/architecture-and-nonfunctional-requirements/6-onboarding) provides additional information on how 'adaptors' may be used to translate an existing API to the patterns described.

## 8.1 Sending emails

### 8.1.1 Sending single emails one by one

This API is designed to send out emails one by one.

Although an email can be sent to multiple recipients by using `email`, `emailCC` and `emailBCC` appropriately, this is still considered as sending a single email.

#### 8.1.1.1 Sample user story

```
AS A Doctor working in a hospital
I WANT TO notify my patient about a confirmed registration
SO THAT the patient would know when to come for a visit
```

#### 8.1.1.2 API endpoint

`POST` `/send/email/single`

```json
{
  "callback": {
    "URI": "https://example.com/callback/emails/requestUID"
  },
  "senderInfo": {
    "organisationName": "Example Medical Insitution",
    "organisationRegNr": "GOV1234567890",
    "onBehalfOfName": "Example Medical Insitution",
    "onBehalfOfRegNr": "GOV1234567890",
    "email": "sender@example.com",
    "replyTo": "reply-to@example.com",
    "name": "Example Doctor"
  },
  "recipientInfo": {
    "email": "customer@example.com",
    "emailCC": "customer-cc@example.com",
    "emailBCC": "customer-bcc@example.com",
    "name": "Example Customer"
  },
  "emailContent": {
    "encoding": "UTF-8",
    "title": "Example Title Of An Email",
    "content": "Example Customer"
  }
}
```

### 8.1.2 Sending multiple (batch) emails at once

This API is designed to send out identical emails to multiple (batch) recipients at once.

#### 8.1.2.1 Sample user story

```
AS A Hospital
I WANT TO notify a specified group of my clients about the possibility to register to vacant time slots within a limited period of time
SO THAT the clients potentially needing it the most would have a guaranteed chance to get an appointment
```

#### 8.1.2.2 API endpoint

Information about recipients is provided as `JSON` in `base64` format.

`POST` `/send/email/batch`

```json
{
  "callbackURI": {
    "URI": "https://example.com/callback/emails/requestUID"
  },
  "senderInfo": {
    "organisationName": "Example Medical Insitution",
    "organisationRegNr": "GOV1234567890",
    "onBehalfOfName": "Example Medical Insitution",
    "onBehalfOfRegNr": "GOV1234567890",
    "email": "sender@example.com",
    "replyTo": "reply-to@example.com",
    "name": "Example Doctor"
  },
  "recipientInfo": {
    "batchEmailAsBase64": "W3sKCSJyZWNpcGllbnRJbmZvIjogewoJCSJlbWFpbCI6ICJjdXN0b21lckBleGFtcGxlLmNvbSIsCgkJImVtYWlsQ0MiOiAiY3VzdG9tZXItY2NAZXhhbXBsZS5jb20iLAoJCSJlbWFpbEJDQyI6ICJjdXN0b21lci1iY2NAZXhhbXBsZS5jb20iLAoJCSJuYW1lIjogIkV4YW1wbGUgQ3VzdG9tZXIiCgl9Cn0sIHsKCSJyZWNpcGllbnRJbmZvIjogewoJCSJlbWFpbCI6ICJkZWFyLWN1c3RvbWVyQGV4YW1wbGUuY29tIiwKCQkibmFtZSI6ICJVbmtub3duIEN1c3RvbWVyIgoJfQp9XQ=="
  },
  "emailContent": {
    "encoding": "UTF-8",
    "title": "Example Title Of An Email",
    "content": "Example Customer"
  }
}
```

### 8.1.3 Responding to emails

This API is designed to accept responses to emails that have been previously sent out by using the Messaging Building Block.

The protocol itself is lightweight and expects custom services from anyone using it. The Messaging Building Block is responsible for delivering the message and does not know (or want to know) anything about the content of it, how it will be used, etc.

#### 8.1.3.1 Sample user story

```
AS A Hospital
I WANT TO get and send responses from and to clients
SO THAT I could continue and keep track of email conversations taken place via GovStack
```

#### 8.1.3.2 API endpoint

`POST` `/callback/email`

```json
{
  "meta": "Meta-info",
  "content": "Q2xpZW50LXNwZWNpZmljIGNvbnRlbnQsIG1vc3QgbGlrZWx5IEpTT04="
}
```

### 8.1.4 Reading the status of emails

This API is designed to provide information about the status of emails sent to the Messaging Building Block.

#### 8.1.4.1 Sample user story

```
AS A Doctor working in a hospital
I WANT TO know which emails I've sent haven't reached their destination
SO THAT I could contact such patients by using different means
```

#### 8.1.4.2 API endpoint

`GET` `/status/email?status=<status_1>&status=<status_2>`

#### 8.1.4.3 States of emails

Possible states of emails that can be queried are as follows:

1. `scheduled`
2. `processing`
3. `deferred`
4. `bounced`
5. `not sent`
6. `delivered`

There is no keeping track of emails which have been sent successfully, as this would end up creating and maintaining a massive database of emails, their senders and recipients, etc., which would be wrong for so many reasons.
