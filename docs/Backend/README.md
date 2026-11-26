# AcquaCEG Backend

🌐 **Language**

- 🇺🇸 **English** (Current)
- 🇧🇷 [Português](READMEinPT-BR.md)

## Overview

The AcquaCEG Backend is the service responsible for processing, storing, and providing access to data collected by the project's IoT devices.

Its main purpose is to receive sensor measurements through MQTT, validate incoming data, store readings in PostgreSQL, and expose the information through a REST API.

The backend works as the communication layer between embedded devices and visualization applications.

---

# Purpose

The backend is responsible for:

- Receiving sensor data from IoT devices;
- Validating incoming information;
- Persisting measurements;
- Providing data through HTTP APIs;
- Supporting future AcquaCEG ecosystem expansions.

---

# Technologies

| Technology | Purpose |
|------------|---------|
| Python | Main language |
| FastAPI | REST API framework |
| Uvicorn | ASGI server |
| Paho MQTT | MQTT communication |
| Pydantic | Data validation |
| SQLAlchemy | ORM |
| PostgreSQL | Database |
| python-dotenv | Configuration management |

---

# Backend Architecture

```text
MQTT Broker

      │

      ▼

 MQTT Service

      │

      ▼

Sensor Service

      │

      ▼

Sensor Repository

      │

      ▼

PostgreSQL Database


      │

      ▼

 REST API
```

---

# Data Flow

1. IoT devices collect sensor measurements.

2. Firmware publishes data through MQTT.

3. The MQTT broker forwards messages to the backend.

4. The backend validates the payload.

5. Data is processed and stored.

6. Applications access information through the REST API.

---

# API

Main endpoints:

| Method | Endpoint | Description |
|-|-|-|
| GET | `/` | Service status |
| GET | `/api/sensors/latest` | Latest reading |
| GET | `/api/sensors/readings` | Reading history |
| GET | `/api/sensors/readings/{id}` | Specific reading |
| DELETE | `/api/sensors/readings/{id}` | Delete reading |

---

# Future Improvements

- Database migrations with Alembic;
- Authentication and authorization;
- Improved observability;
- Physical unit conversion;
- Expanded test coverage;
- Device monitoring.
