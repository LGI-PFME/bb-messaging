---
description: >-
  Key Digital Functionalities describe the core (required) functions that this
  Building Block must be able to perform.
---

# 4 Key Digital Functionalities

The Messaging Building Block is a standalone messaging gateway/client/proxy (including all possible modalities: email, SMS, etc.) but can also facilitate connections with existing messaging service providers by enabling safe communication. The communication in this Building Block can be categorized in two different directions as follows:

## 4.1 Government to person (G2P) <a href="#docs-internal-guid-c38a9447-7fff-fcb5-e6eb-c6419072f004" id="docs-internal-guid-c38a9447-7fff-fcb5-e6eb-c6419072f004"></a>

* informing End clients about their registration;
* reminding and requesting End clients' confirmation for appointment booking or other events;
* delivering information at scale to End clients;
* alerting End clients in emergency contexts.

## 4.2 Person to Government (P2G) <a href="#docs-internal-guid-c38a9447-7fff-fcb5-e6eb-c6419072f004" id="docs-internal-guid-c38a9447-7fff-fcb5-e6eb-c6419072f004"></a>

* providing data to the government/service;
* getting confirmation about government services and interactions quickly;
* asking for information about government services.

Communication between different government services (government to government) is out of the scope of this Building Block but can be enabled through the Information Mediator Building Block.

## 4.3 Out-of-Scope Assumptions

* Scheduling messages according to some business logic is out of the scope of this Building Block because is done by Scheduler Building Block.
* Processing of incoming message content to apply some business logic.
* Fully offline and no internet connection scenarios.
* Real-time video and audio conferencing.
