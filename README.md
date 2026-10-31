# AcquaCEG

> Smart water quality monitoring ecosystem powered by IoT, cloud computing and embedded systems.

---

## 🇺🇸 English

### Overview

AcquaCEG is an open-source ecosystem for real-time water quality monitoring, combining embedded systems, IoT, cloud computing and modern software engineering.

The project aims to collect data from water quality sensors, process the information in the cloud and provide reliable monitoring through web and mobile applications.

Although initially designed for healthcare water treatment environments, the architecture was developed to be flexible enough for future applications in laboratories, industrial processes, educational projects and environmental monitoring.

---

## Inspiration

The project was inspired by my father's daily work with water treatment systems.

The name **AcquaCEG** is also a tribute to him, being derived from his initials:

**Carlos Eduardo Guimarães (CEG)**

The idea was born from observing the importance of continuously monitoring water quality and the need for affordable, intelligent and connected monitoring solutions.

---

## Project History

- 📅 **June 2026** — Project started.
- 🎓 **2026** — The first version of AcquaCEG was presented during the **VISITE** exhibition at **ETEC Fernando Prestes**, together with the development team.
- 🛠️ The version presented at the event is now maintained as the **Legacy** version of the project.
- 🚀 The current generation is being redesigned with a modern cloud architecture based on IoT technologies.

---

# Current Architecture

```text
                     Sensors
          pH • Conductivity • Temperature • Water Level
                           │
                           ▼
              Arduino Uno R4 WiFi (Firmware)
                           │
                     MQTT over TLS
                           │
                           ▼
                      EMQX Cloud Broker
                           │
                           ▼
                  FastAPI Backend (Python)
                           │
             Data Validation & Processing
                           │
                           ▼
                     PostgreSQL Database
                           │
                           │
                          ▼                                 
                     REST API                       
                          │
                     ┌────┴────┐
                     ▼         ▼
                 Web Dashboard   Mobile Application
```

---

## Communication Flow

1. Sensors collect water quality measurements.
2. The firmware running on the Arduino processes the raw sensor readings.
3. Measurements are published to the MQTT broker.
4. The FastAPI backend subscribes to the MQTT topics.
5. Incoming data is validated and converted into engineering units.
6. Valid measurements are stored in PostgreSQL.
7. Applications access the information through the REST API.
8. Future versions will include notifications, dashboards and AI-assisted monitoring.

---

# Repository Structure

| Repository | Description 
|------------|-------------
| **AcquaCEG** | Main documentation and project overview 
| **Firmware** | Embedded firmware running on Arduino 
| **Backend** | FastAPI API, MQTT integration and database 
| **Mobile** | Mobile monitoring application *(future)* 
| **Web** | Monitoring dashboard *(future)* 
| **Legacy** | First generation of the project 

---

# Technologies

## Embedded Systems

- Arduino Uno R4 WiFi
- PlatformIO
- C++

## Communication

- MQTT
- EMQX Cloud

## Backend

- Python
- FastAPI
- SQLAlchemy
- PostgreSQL

## Cloud

- Google Cloud *(planned)*

## Mobile

- Dart *(planned)*

---

# Project Goals

- Continuous water quality monitoring
- Modular architecture
- Cloud-native communication
- Open-source development
- Educational and research purposes
- Healthcare and industrial applications

---

# Development Status

| Module | Status |
|---------|--------|
| Firmware | 🚧 In Development |
| Backend | 🚧 In Development |
| Cloud Infrastructure | 📅 Planned |
| Mobile App | 📅 Planned |
| Web Dashboard | 📅 Planned |
| PCB | 📅 Planned |

---

# License

This project is distributed under the MIT License.

---

# 🇧🇷 Português

## Visão Geral

O AcquaCEG é um ecossistema open source para monitoramento da qualidade da água em tempo real, unindo sistemas embarcados, Internet das Coisas (IoT), computação em nuvem e engenharia de software moderna.

O objetivo é coletar dados de sensores de qualidade da água, processá-los na nuvem e disponibilizar essas informações para aplicações web e móveis.

Embora tenha sido inicialmente pensado para ambientes relacionados ao tratamento de água na área da saúde, sua arquitetura foi desenvolvida para permitir aplicações futuras em laboratórios, processos industriais, pesquisa e monitoramento ambiental.

---

## Inspiração

O projeto nasceu inspirado no trabalho diário do meu pai com sistemas de tratamento de água.

Seu nome também é uma homenagem a ele.

**AcquaCEG**

Onde **CEG** representa suas iniciais:

**Carlos Eduardo Guimarães**

A ideia surgiu da observação da importância do monitoramento contínuo da qualidade da água e da necessidade de soluções inteligentes, acessíveis e conectadas.

---

## História do Projeto

- 📅 **Junho de 2026** — início do desenvolvimento.
- 🎓 **2026** — apresentação da primeira versão durante o evento **VISITE**, da **ETEC Fernando Prestes**, juntamente com toda a equipe de desenvolvimento.
- 🛠️ A versão apresentada passou a ser mantida como a versão **Legacy** do projeto.
- 🚀 Atualmente o sistema está sendo reconstruído com uma arquitetura moderna baseada em IoT e computação em nuvem.

---

# Arquitetura Atual

```text
Sensores
(pH • Condutividade • Temperatura • Nível de Água)
                │
                ▼
Arduino Uno R4 WiFi
                │
             MQTT
                │
                ▼
          EMQX Cloud
                │
                ▼
      Backend FastAPI
                │
     Validação dos Dados
                │
                ▼
          PostgreSQL
                │
                │
                ▼                   
           REST API             
                │
           ┌────┴────┐
           ▼         ▼
      Dashboard   Aplicativo Mobile
```

---

## Fluxo de Comunicação

1. Os sensores realizam as medições da água.
2. O firmware processa os sinais coletados.
3. Os dados são enviados via MQTT.
4. O backend recebe essas informações.
5. Os valores são validados e convertidos.
6. As leituras são armazenadas no PostgreSQL.
7. As aplicações consomem os dados através da API REST.
8. Futuramente o sistema contará com dashboards, notificações e recursos baseados em IA.

---

# Estrutura dos Repositórios

| Repositório | Descrição |
|-------------|-----------|
| **AcquaCEG** | Documentação principal do projeto |
| **Firmware** | Firmware embarcado |
| **Backend** | API, MQTT e banco de dados |
| **Mobile** | Aplicativo móvel *(futuro)* |
| **Web** | Dashboard *(futuro)* |
| **Legacy** | Primeira geração do projeto |

---

# Tecnologias

## Sistemas Embarcados

- Arduino Uno R4 WiFi
- PlatformIO
- C++

## Communicação

- MQTT
- EMQX Cloud

## Backend

- Python
- FastAPI
- SQLAlchemy
- PostgreSQL

## Cloud

- Google Cloud *(planned)*

## Mobile

- Dart *(planned)*

---

# Objetivos

- Monitoramento contínuo da qualidade da água
- Arquitetura modular
- Comunicação baseada em nuvem
- Desenvolvimento open source
- Aplicações em pesquisa
- Aplicações hospitalares e industriais

---

# Licença

Distribuído sob a licença MIT.
