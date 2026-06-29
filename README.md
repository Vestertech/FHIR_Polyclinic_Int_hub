# 🏥 Polyclinic FHIR Integration Hub

A complete FHIR server demonstration built on the [HAPI FHIR JPA Server Starter](https://github.com/hapifhir/hapi-fhir-jpaserver-starter) project. This repository contains **my custom configuration, documentation, and workflows** that showcase real-world healthcare interoperability.

> **Note:** This repository is **my project documentation and configuration**, not a fork of the starter project. The actual FHIR server runs from the official Docker image `hapiproject/hapi:latest`. My contributions are the custom configuration, clinical workflows, and API documentation.

---

## 📌 Project Overview

This project demonstrates **FHIR R4 interoperability** using the HAPI FHIR JPA Server with:

- **Patient Registration** with Ontario Health Card extension
- **Clinical Referral Workflows** (Patient → Practitioner → ServiceRequest)
- **Lab Ordering & Diagnostic Reporting** (Observation → DiagnosticReport)
- **CRUDV Operations** with optimistic locking
- **Advanced FHIR Patterns**: $everything, chained searches, batch transactions

### What I Built vs. What the Starter Provides

| Component | Source | My Contribution |
|-----------|--------|-----------------|
| **FHIR Server Engine** | [HAPI FHIR Starter](https://github.com/hapifhir/hapi-fhir-jpaserver-starter) | Used as base |
| **Docker Configuration** | Starter documentation | Custom `docker-compose.yml` |
| **Server Settings** | Starter defaults | Custom `hapi.application.yaml` |
| **Clinical Workflows** | N/A | Designed and implemented |
| **API Documentation** | N/A | Postman collection with saved responses |
| **Ontario Health Card Extension** | N/A | Custom FHIR extension |

---

## 🚀 Quick Start

### Prerequisites

- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [Postman](https://www.postman.com/downloads/) (for API testing)

### Run the FHIR Server

```bash
# Clone this repository
git clone https://github.com/Vestertech/FHIR_Polyclinic_Int_hub.git
cd FHIR_Polyclinic_Int_hub

# Start the server using Docker Compose
docker-compose up -d

# Wait 30 seconds for startup



Access Points
| Servive | URL |  
|-----------|--------|
| **FHIR Server Base** | [HAPI FHIR](	http://localhost:8080/fhir) 
| **Postman Documentation** | [My documentation]([https://documenter-api.postman.tech/view/23083428/2sBXwyHSo4](https://documenter.getpostman.com/view/23083428/2sBXwyHSo4))|
| **CapabilityStatements** | [Link](http://localhost:8080/fhir/metadata) |
| **Web UI** | [WebURL ](http://localhost:8080/)|

📚 API Documentation
Published Postman Documentation
👉- [View the Complete Postman Documentation](https://www.postman.com/downloads/)

This interactive documentation includes:

All 15+ FHIR endpoints with descriptions

Request/response examples

Clinical workflow scenarios

Environment variables setup

Import to Postman
Download Polyclinic Integration Hub postman_collection.json from this repository

Open Postman → Click "Import"

Upload the JSON file

Set environment variable baseUrl to http://localhost:8080/fhir

Swagger UI (OpenAPI)
Interactive API documentation is available at:
http://localhost:8080/fhir/swagger-ui/

🏗️ Architecture & Design
This project is built on the HAPI FHIR JPA Server Starter, which provides:

JPA-based persistence with H2/PostgreSQL

FHIR R4 resource providers

Interceptor framework for custom logic

Spring Boot application

Project Structure
📁 FHIR_Polyclinic_Int_hub/
├── docker-compose.yml              # Docker Compose configuration
├── hapi.application.yaml           # Custom FHIR server settings
├── Polyclinic Integration Hub postman_collection.json  # Postman collection
├── README.md                       # Project documentation

🔬 FHIR Workflows Demonstrated
1. Patient Registration (with Custom Extension)
Purpose: Demonstrate FHIR's extensibility model

Request:
POST {{baseUrl}}/Patient

Body:
{
  "resourceType": "Patient",
  "extension": [
    {
      "url": "http://ontariohealth.ca/fhir/StructureDefinition/health-card",
      "valueIdentifier": {
        "system": "http://ontariohealth.ca/health-card",
        "value": "AB1234567890"
      }
    }
  ],
  "name": [{"family": "Rodriguez", "given": ["Maria"]}],
  "gender": "female",
  "birthDate": "1975-03-15"
}
Real-World Scenario: New patient registration with Ontario Health Card for billing.

2. Referral Workflow
Purpose: Link Patient, Requester, and Performer

Request:
POST {{baseUrl}}/ServiceRequest
Body:
{
  "resourceType": "ServiceRequest",
  "subject": {"reference": "Patient/{{patientId}}"},
  "requester": {"reference": "Practitioner/DR-CHEN"},
  "performer": [{"reference": "Practitioner/DR-JONES"}],
  "code": {
    "coding": [{
      "system": "http://snomed.info/sct",
      "code": "408520003",
      "display": "Consultation for hypertension"
    }]
  }
}

3. Lab Order & Results
Complete Workflow:

Create ServiceRequest (lab order)

Create Observations (individual lab results)

Create DiagnosticReport (aggregates results)

$everything gets complete record

4. Advanced FHIR Operations
Operation	|Description |	Example
$everything |	Get complete patient | record	GET {{baseUrl}}/Patient/{{id}}/$everything
Chained Search	| Find patients by practitioner | 	GET {{baseUrl}}/Patient?_has:ServiceRequest:subject:requester=Practitioner/DR-CHEN
Batch Transaction |	Atomic multiple operations	| POST {{baseUrl}} (Bundle type: transaction)
Optimistic Locking	| Prevent lost updates	| Uses meta.versionId in PUT requests


📖 Source & Acknowledgments
This project is built on the HAPI FHIR JPA Server Starter (https://github.com/hapifhir/hapi-fhir-jpaserver-starter) by the HAPI FHIR team.

Starter Project: hapifhir/hapi-fhir-jpaserver-starter(https://github.com/hapifhir/hapi-fhir-jpaserver-starter)

Official Image: hapiproject/hapi:latest (https://hub.docker.com/r/hapiproject/hapi)

Documentation: HAPI FHIR Documentation (https://hub.docker.com/r/hapiproject/hapi)

What I Added
Custom application.yaml with OpenAPI/Swagger enabled

Docker Compose configuration for easy deployment

Complete Postman collection with 15+ documented workflows

Ontario Health Card custom FHIR extension

Clinical workflows (referrals, lab ordering, diagnostic reporting)
