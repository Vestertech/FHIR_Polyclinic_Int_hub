# 🏥 Polyclinic FHIR Integration Hub

A complete FHIR server implementation demonstrating interoperability workflows using HAPI FHIR JPA Server. This project showcases practical application of Digital Health Architecture principles through real-world clinical workflows.

## 📌 Project Overview

This project deploys a **FHIR R4 server** using the HAPI FHIR JPA Starter [citation:2] and demonstrates:

- **Standards-Based Interoperability**: HL7 FHIR RESTful API with CRUDV operations [citation:4]
- **Clinical Workflows**: Patient registration, referrals, lab ordering, diagnostic reporting
- **Advanced FHIR Patterns**: Extensions, resource references, chained searches, batch transactions [citation:5]
- **Production-Ready Configuration**: Docker Compose, PostgreSQL support, OpenAPI documentation [citation:2]

> **What We Built**: This isn't a basic CRUD demo. It's a fully functional FHIR server with custom extensions (Ontario Health Card), multi-resource workflows (Patient → Practitioner → ServiceRequest → Observation → DiagnosticReport), and complete API documentation via Postman and Swagger.

## 🚀 Quick Start

### Prerequisites
- Docker Desktop (or Docker + Docker Compose)
- Postman (for API testing)

### Run the FHIR Server

```bash
# Clone this repository
git clone https://github.com/Vestertech/FHIR_Polyclinic_Int_hub.git
cd hapi-fhir-polyclinic-hub

# Start the server
docker-compose up -d

# Wait 30 seconds for startup
