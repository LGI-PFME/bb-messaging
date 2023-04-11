---
description: >-
  Key Digital Functionalities describe the core (required) functions that this
  Building Block must be able to perform.
---

# 4 Key Digital Functionalities

## 4.1 Overview of Messaging Building Block Functionality

The Messaging Building Block is a standalone messaging gateway/client/proxy (including all possible modalities: email, SMS, etc.), but can also facilitate connections with existing messaging service providers by enabling safe communication. The communication in this Building Block can be categorized  in two different directions as follows:

* Government to person (G2P):
  * informing citizens about their registration;
  * reminding and requesting citizens' confirmation for appointment booking or other events;
  * delivering information at scale to citizens;
  * alerting citizens in emergency contexts.
* Person to Government (P2G):
  * providing data to the government/service;
  * getting confirmation about government services and interactions quickly;
  * asking for information about government services.

Communication between different government services (government to government) is out of the scope of this Building Block but can be enabled through the Information Mediator Building Block.

## 4.2 Design and Components of Messaging Building Block <a href="#docs-internal-guid-d85f59a4-7fff-1564-6ae2-86d67f36a258" id="docs-internal-guid-d85f59a4-7fff-1564-6ae2-86d67f36a258"></a>

1. The Messaging Building Block is part of the GovStack implementation and is prompted to open up a two-way communication channel to deliver and capture messages/data between the GovStack systems and the end users, physical and legal persons.
2. As a rule, the Messaging Building Block does not own any information but is carrying the minimum amount of (meta) data needed to transfer/publish a message. Messaging Building Block allows other Building Blocks and applications to reach out to customers/citizens in order for them to be able to make a decision or access a service. This Building Block can also be used for broadcasting a disaster message.
3. Messaging policies are configurable modalities and channels that can be accessed/utilized through the Messaging Building Block in order to reach out to the users or groups. This Building Block is using existing applications/channels, such as e-mail, SMS, and messaging platforms for enabling users to subscribe to an application/channel provided by Messaging Building Block itself for text-based content.
4. Having published its messaging policies and services at the Information Mediator Building Block, the other Building Blocks and applications can discover and use the services of the Messaging Building Block.
5. Messaging Building Block allows for asynchronous communication, using either point-to-point communication or a Pub/Sub model (using Information Mediator Building Block) where the user is subscribed to a message room/group and will be receiving all messages intended for the “mother of newborn child” group.
6. Security. Before allowing any messages to be published, the Messaging Building Block fetches a corresponding ID and a role or a session token available for the user for authentication and access purposes. Incorporates privacy into its design when the purpose of the authentication is not revealed if a service provider sends an authentication request.
