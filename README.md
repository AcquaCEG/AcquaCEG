# 💧 AcquaCEG

> Monitoramento Inteligente. Água Preservada.

O **AcquaCEG** é um ecossistema open source para monitoramento da qualidade da água utilizando Internet das Coisas (IoT), sistemas embarcados e computação em nuvem.

Este repositório centraliza a documentação oficial, a arquitetura do sistema, diagramas, decisões de projeto e informações gerais sobre todo o ecossistema AcquaCEG.

---

# 📖 Sobre o projeto

O objetivo do AcquaCEG é fornecer uma plataforma modular para aquisição, processamento e visualização de dados provenientes de sensores de qualidade da água.

A arquitetura foi projetada para permitir que diferentes componentes evoluam de forma independente, mantendo uma comunicação padronizada entre firmware, backend e aplicações cliente.

---

# 🏗 Arquitetura Geral

```text
Sensores
    │
    ▼
Firmware (Arduino / ESP32)
    │
    ▼
Broker MQTT
    │
    ▼
Backend (FastAPI)
    │
    ▼
PostgreSQL
    │
    ▼
REST API
    │
    ▼
Frontend / Dashboard
```

---

# 📚 Documentação

Toda a documentação do projeto encontra-se na pasta **docs/**.

Ela inclui:

- Arquitetura do sistema
- Backend
- Firmware
- Frontend
- Hardware
- API
- Diagramas
- Roadmap
- Decisões de projeto

---

# 📦 Repositórios

| Repositório | Descrição |
|-------------|-----------|
| AcquaCEG | Documentação oficial do projeto |
| AcquaCEG-Backend | API REST e processamento das leituras |
| AcquaCEG-Firmware | Firmware dos dispositivos IoT |
| AcquaCEG-Frontend | Interface Web |

---

# 🎯 Objetivos

- Monitoramento em tempo real
- Arquitetura modular
- Fácil manutenção
- Código aberto
- Escalabilidade
- Base para pesquisa e desenvolvimento

---

# 📄 Licença

Este projeto é distribuído sob a licença MIT.

---

# 👨‍💻 Organização

Desenvolvido pela organização **AcquaCEG**.

In English Now

# 💧 AcquaCEG

> Smart Monitoring. Water Preserved.

AcquaCEG is an open-source ecosystem for water quality monitoring based on the Internet of Things (IoT), embedded systems, and cloud computing.

This repository serves as the central hub for the project's official documentation, system architecture, design decisions, diagrams, and general information.

---

# 📖 About

The goal of AcquaCEG is to provide a modular platform for collecting, processing, and visualizing water quality data from embedded devices.

The architecture is designed to allow each component to evolve independently while maintaining standardized communication between firmware, backend, and client applications.

---

# 🏗 System Architecture

```text
Sensors
    │
    ▼
Firmware (Arduino / ESP32)
    │
    ▼
MQTT Broker
    │
    ▼
Backend (FastAPI)
    │
    ▼
PostgreSQL
    │
    ▼
REST API
    │
    ▼
Frontend / Dashboard
```

---

# 📚 Documentation

The complete project documentation is available inside the **docs/** directory.

It includes:

- System Architecture
- Backend
- Firmware
- Frontend
- Hardware
- API
- Diagrams
- Roadmap
- Architecture Decision Records (ADR)

---

# 📦 Repositories

| Repository | Description |
|------------|-------------|
| AcquaCEG | Official project documentation |
| AcquaCEG-Backend | REST API and data processing |
| AcquaCEG-Firmware | IoT device firmware |
| AcquaCEG-Frontend | Web interface |

---

# 🎯 Goals

- Real-time monitoring
- Modular architecture
- Easy maintenance
- Open source
- Scalability
- Research and educational purposes

---

# 📄 License

This project is licensed under the MIT License.

---

# 👨‍💻 Organization

Developed by the **AcquaCEG** organization.
