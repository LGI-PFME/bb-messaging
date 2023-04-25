---
description: >-
  This section provides information on the core data structures/data models that
  are used by this Building Block.
---

# 7 Data Structures

## 7.1 Resource Model

The resource model shows the relationship between data objects that are used by this Building Block.

<figure><img src=".gitbook/assets/7 Data Structures.png" alt=""><figcaption><p><em>Note: Recommend using</em> <a href="https://app.diagrams.net/"><em>https://app.diagrams.net/</em></a> <em>to create the resource model and store in Building Block repository (</em><a href="https://github.com/GovStackWorkingGroup/bb-messaging/tree/1.0-QA/api"><em>https://github.com/GovStackWorkingGroup/bb-messaging/tree/1.0-QA/api</em></a><em>)</em></p></figcaption></figure>

## 7.2 Data Structures

### 7.2.1 Data Elements (Generic Example)

**7.2.1.1 Person**

| Name                 | Type     | Description                   | Notes                                                                                              |
| -------------------- | -------- | ----------------------------- | -------------------------------------------------------------------------------------------------- |
| **Name**             | **Type** | **Description**               | **Notes**                                                                                          |
| Surname              | String   | Family name                   |                                                                                                    |
| First Name           | String   | First name                    |                                                                                                    |
| Birth Date           | Date     | DOB                           | [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)                                 |
| Mobile Number        | String   | Phone number (mobile) of user | [E.164 Mobile number standard](https://www.itu.int/rec/T-REC-E.164/). Should include country code. |
| Government ID number | Integer  | Government issued ID number   | Used when linking to global ID Building Block.                                                     |

### Standards

The following standards are applicable to data structures in the Messaging Building Block:

* all services are provided as REST API requests;
* only Transport Layer Security (TLS) Server Name Indication (SNI) extension-compatible requests are allowed;
* REST calls and responses use JSON as the only allowed data format.

1. Using [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) on dates and times is a MUST;
2. [UTF-8 character encoding](https://en.wikipedia.org/wiki/UTF-8) on text input is a MUST.

### **Model Schemas**

Each model schema MUST have a corresponding JSON Schema ([API definition file](https://raw.githubusercontent.com/GovStackWorkingGroup/BuildingBlockAPI/main/ExampleSchema.json)).
