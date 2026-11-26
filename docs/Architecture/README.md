🌐 Language

- 🇺🇸 English (current)
- 🇧🇷 [Português](READMEinPT-BR.md)

# System Architecture

## Overview

The AcquaCEG architecture is designed with a modular approach, separating responsibilities between data acquisition, communication, processing, persistence, and data visualization.

The system is currently composed of three main modules:

- Firmware
- Backend
- Frontend

Each module can evolve independently while communicating through well-defined protocols and interfaces.

---

# Overall Architecture

```text
                  Sensors
      (Temperature, pH,
   Conductivity, Water Level)

                  │
                  ▼
        AcquaCEG Firmware
       (Arduino Uno R4 WiFi)
                  │
          MQTT over TLS
                  │
                  ▼
          EMQX Cloud Broker
                  │
                  ▼
        AcquaCEG Backend
         FastAPI + MQTT
                  │
          SQLAlchemy ORM
                  │
                  ▼
             PostgreSQL
                  │
             REST API
                  │
                  ▼
       Frontend / Dashboard
```

---

# Data Flow

A complete sensor reading follows the workflow below:

1. The firmware collects data from the connected sensors.

2. The measurements are formatted into a JSON payload.

3. The firmware publishes the data to the MQTT broker using a secure TLS connection.

4. The backend subscribes to the configured MQTT topic.

5. When a new message is received, the backend:

- validates the JSON payload;
- validates the data using Pydantic schemas;
- identifies the device from the MQTT topic;
- converts the payload into the internal data model.

6. The validated reading is stored in PostgreSQL using SQLAlchemy.

7. The data becomes available through the REST API.

8. The frontend retrieves the information from the API and presents it to the user.

---

# Components

## Firmware

Responsible for:

- Reading sensor data;
- Managing the Wi-Fi connection;
- Publishing measurements through MQTT.

---

## MQTT Broker

Responsible for:

- Receiving messages from IoT devices;
- Delivering messages to the backend;
- Decoupling firmware from backend services.

---

## Backend

Responsible for:

- Consuming MQTT messages;
- Validating incoming data;
- Persisting sensor readings;
- Providing the REST API.

---

## Database

Responsible for storing all sensor readings received by the backend.

The current implementation uses PostgreSQL.

---

## Frontend

Responsible for displaying the data exposed by the REST API.

---

# Architectural Principles

The AcquaCEG architecture follows the following principles:

- Modularity
- Separation of Concerns
- Low Coupling
- Maintainability
- Scalability
- Event-Driven Communication (MQTT)

---

# Component Communication

| Source | Destination | Technology |
|---------|-------------|------------|
| Firmware | MQTT Broker | MQTT over TLS |
| MQTT Broker | Backend | MQTT |
| Backend | PostgreSQL | SQLAlchemy |
| Frontend | Backend | HTTP REST |

---

# Current Capabilities

The current architecture supports:

- Receiving sensor readings through MQTT;
- Validating incoming messages;
- Persisting data into PostgreSQL;
- Retrieving historical readings through the REST API;
- Retrieving the latest sensor reading;
- Deleting stored readings through the REST API.

The architecture has been designed to support future expansion while preserving the current modular structure.