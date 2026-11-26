🌐 Idioma

- 🇧🇷 Português (atual)
- 🇺🇸 [English](README.md)

# Arquitetura do Sistema

## Visão Geral

A arquitetura do AcquaCEG foi projetada de forma modular para separar as responsabilidades entre aquisição de dados, comunicação, processamento, persistência e disponibilização das informações.

Atualmente, o sistema é composto por três módulos principais:

- Firmware
- Backend
- Frontend

Cada módulo pode evoluir de forma independente, comunicando-se através de protocolos e interfaces bem definidos.

---

# Arquitetura Geral

```text
                 Sensores
        (Temperatura, pH,
      Condutividade, Nível)

                 │
                 ▼
        AcquaCEG Firmware
        (Arduino Uno R4 WiFi)
                 │
        MQTT (TLS)
                 │
                 ▼
          Broker EMQX Cloud
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

# Fluxo dos Dados

O ciclo completo de uma leitura ocorre da seguinte forma:

1. O firmware realiza a leitura dos sensores conectados ao dispositivo.

2. Os dados são organizados em formato JSON.

3. O firmware publica a leitura no broker MQTT utilizando conexão TLS.

4. O backend permanece inscrito no tópico configurado.

5. Ao receber uma nova mensagem:

- valida o JSON;
- valida os campos utilizando Pydantic;
- identifica o dispositivo através do tópico MQTT;
- converte os dados para o modelo interno.

6. A leitura é persistida no PostgreSQL através do SQLAlchemy.

7. Os dados ficam disponíveis através da API REST.

8. O frontend consulta a API para apresentar as informações ao usuário.

---

# Componentes

## Firmware

Responsável por:

- leitura dos sensores;
- conexão Wi-Fi;
- comunicação MQTT;
- publicação das medições.

---

## Broker MQTT

Responsável por:

- receber mensagens dos dispositivos;
- entregar mensagens ao backend;
- desacoplar firmware e backend.

---

## Backend

Responsável por:

- consumir mensagens MQTT;
- validar dados;
- persistir leituras;
- disponibilizar API REST.

---

## Banco de Dados

Responsável por armazenar todas as leituras recebidas.

Atualmente utiliza PostgreSQL.

---

## Frontend

Responsável pela visualização dos dados disponibilizados pela API REST.

---

# Princípios da Arquitetura

A arquitetura do AcquaCEG segue alguns princípios:

- Modularidade
- Separação de responsabilidades
- Baixo acoplamento
- Fácil manutenção
- Escalabilidade
- Comunicação baseada em eventos (MQTT)

---

# Comunicação entre Componentes

| Origem | Destino | Tecnologia |
|---------|----------|------------|
| Firmware | Broker | MQTT sobre TLS |
| Broker | Backend | MQTT |
| Backend | PostgreSQL | SQLAlchemy |
| Frontend | Backend | HTTP REST |

---

# Estado Atual

Atualmente o sistema permite:

- Receber leituras MQTT.
- Validar mensagens recebidas.
- Persistir dados no PostgreSQL.
- Consultar histórico pela API REST.
- Consultar a última leitura.
- Remover leituras através da API.

Os módulos foram projetados para permitir futuras expansões sem alterações significativas na arquitetura principal.