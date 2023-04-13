---
description: >-
  This section provides a detailed view of how this Building Block will interact
  with other Building Blocks to support common use cases.
---

# 9 Internal Workflows

A workflow provides a detailed view of how this Building Block will interact with other Building Blocks to support common use cases.

This section lists workflows that this Building Block must support. Other workflows may be implemented in addition to those listed.

## 9.1   Workflow diagram <a href="#_z337ya" id="_z337ya"></a>

### 9.1.1 Prerequisites and dependencies <a href="#_3j2qqm3" id="_3j2qqm3"></a>

The main prerequisite for Person-to-Building Block communication is that there is an existing Sender/Source Building Block with the following properties:

* the relevant credentials and details about the Person/Citizen to be addressed with;
* the content of the message and a reference to a communication channel (contact details) to be used;
* additionally, the service discovery service at the Information Mediator Building Block needs to be active. Information Mediator Building Block publishes the list of available services of the Messaging Building Block to the source GovStack Building Block, i.e. Workflow.

A reference token should be carried throughout the communication session in order to save a point of reference for reverse communication back from the Person to the Building Block. In other words, the main prerequisite for Person-to-Building Block communication is the availability of a communication channel and a reference token.

#### **9.1.1.1      Description**

This generic workflow is used to transfer messages between GovStack Building Block and the end user, Person. Data is submitted from a GovStack Building Block front-end application. This workflow shows a connection to GovStack Building Block (such as a government Health System Application) to convey a message that is associated with a real person.

#### **9.1.1.2      Interaction with Other Building Blocks**

This workflow requires interaction with the Information Mediator Building Block and a source GovStack Building Block, for example, a Health Care Service Building Block or registry Building Block.

#### **9.1.1.3      Sequence Diagram**

The sequence diagram shows the flow of data between Building Blocks for this workflow.

#### Messaging: Government to Person (G2P)

```mermaid
sequenceDiagram

Workflow BB-->>Information Mediator: Trigger event on<br />specific day and time
Information Mediator-->>Messaging BB: Initate request with<br />messaging data
Messaging BB-->>Information Mediator: Confirm message receival<br />and queueing
Messaging BB-->>Communication Channel: Apply rules and policies<br />to process the message
Communication Channel->>Person: Send message
Communication Channel-->>Messaging BB: Publish message status
Messaging BB-->>Information Mediator: Publish message Status
```

#### Messaging: Person to Government (P2G)

```mermaid
sequenceDiagram

Person->>Communication Channel:Send a message
Communication Channel-->>Messaging BB: Send event to client
Messaging BB-->>Communication Channel: Confirm message receival
Messaging BB-->>Information Mediator: Proxy event to<br />Information Mediator
Information Mediator-->>Workflow BB: Proxy event to be handled<br />by Workflow BB
```

## **9.2 Interactions**

### **9.2.1 Government/BB to Person communication**



| Sender Building Block: Identification of the Recipient /Person | <p>Sender/Publisher Building Block service application to retrieve relevant</p><p>Person and Contact Channel Data.</p> | Data structure may contain additional elements.                                                                                       |
| -------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| Validate Person and Contact Channel Data                       | Link to appropriate data structure in the relevant GovStack Building Block (Registry/Service).                         | Inform the user if a record already exists and return a unique identifier.                                                            |
| Internal De-duplication Search                                 | Person and Contact Channel Data Structure.                                                                             | Return a ‘Record Exists’ message to the user if it is already in the registration database.                                           |
| Create Message Record                                          | Person and Contact Channel Data Structure.                                                                             | <p>Generate a unique ID for this record (auto-increment).</p><p>Create a unique token to be carried through the delivery process.</p> |
| Publish Message through Communication Channel                  | Communicate Message Data and User ID to Communication Channel.                                                         | Data structure may contain additional elements.                                                                                       |
| Deliver message to the person                                  | Internal Data Structure from the respective channel.                                                                   | Internal Data structure from Communication Channels may contain additional elements.                                                  |
| Publish Status for the original sender                         | User and Message IDs with Delivery Status containing date and time.                                                    | The Message's unique ID is preserved to keep up its status updated.                                                                   |

### **9.2.2** Person to Government/Building Block communication

| Person: Messaging receival from the communication channel                    | Text message and User ID.                                                                                                  | Internal Data structure from Communication Channels may contain additional elements.    |
| ---------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| Communication Channel: Send event to client                                  | Communicate Message Data and User ID to Communication Channel.                                                             | Data structure may contain additional elements.                                         |
| Messaging Building Block: Confirm message receival                           | Message Delivery Data Structure following Communication Channel standards with Status.                                     | The Message unique ID is collected to keep up other statuses updated.                   |
| Information Mediator Building Block: Identification of the Recipient /Person | <p>Information Mediator Building Block service application to retrieve relevant</p><p>Person and Contact Channel Data.</p> | Data structure may contain additional elements.                                         |
| Validate Person and Contact Channel Data                                     | Link to the appropriate data structure in the relevant GovStack Building Block (Registry/Service).                         | Check if the record already exists and return a unique identifier or create one if not. |
