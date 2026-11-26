# AcquaCEG Backend

> 🌐 **Idioma:** [🇺🇸 English](README.md) | 🇧🇷 Português

## Visão Geral

O AcquaCEG Backend é o serviço responsável pelo processamento, armazenamento e disponibilização dos dados coletados pelos dispositivos IoT do projeto.

Sua principal função é receber medições enviadas pelos dispositivos através do protocolo MQTT, validar os dados recebidos, armazená-los em um banco de dados PostgreSQL e disponibilizá-los através de uma API REST.

O backend atua como camada intermediária entre os dispositivos embarcados e as aplicações de visualização.

---

# Objetivo

O backend foi desenvolvido para:

- Receber dados de sensores provenientes dos dispositivos IoT;
- Validar a integridade das informações recebidas;
- Persistir leituras em banco de dados;
- Disponibilizar dados através de uma API HTTP;
- Permitir futuras expansões do ecossistema AcquaCEG.

---

# Tecnologias Utilizadas

| Tecnologia | Função |
|------------|--------|
| Python | Linguagem principal |
| FastAPI | Desenvolvimento da API REST |
| Uvicorn | Servidor ASGI |
| Paho MQTT | Comunicação com broker MQTT |
| Pydantic | Validação dos dados |
| SQLAlchemy | ORM e acesso ao banco |
| PostgreSQL | Banco de dados |
| python-dotenv | Gerenciamento de configurações |

---

# Arquitetura do Backend

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

# Estrutura do Projeto

```text
app/
│
├── api/
│   └── Endpoints HTTP
│
├── core/
│   └── Configurações e dependências
│
├── database/
│   └── Conexão e gerenciamento do banco
│
├── models/
│   └── Modelos ORM
│
├── mqtt/
│   └── Comunicação MQTT
│
├── schemas/
│   └── Validação dos dados
│
├── services/
│   └── Regras de negócio
│
├── repositories/
│   └── Persistência dos dados
│
├── lifespan.py
│   └── Gerenciamento do ciclo de vida
│
└── main.py
    └── Inicialização da aplicação
```

---

# Fluxo de Dados

## Recebimento MQTT

O fluxo de uma leitura ocorre da seguinte maneira:

1. O dispositivo IoT coleta informações dos sensores.

2. O firmware envia os dados em formato JSON através do MQTT.

3. O broker MQTT encaminha a mensagem ao backend.

4. O serviço MQTT recebe a mensagem.

5. O payload é validado utilizando schemas Pydantic.

6. Os dados são processados pelo serviço de aplicação.

7. A leitura é armazenada no PostgreSQL.

---

# Comunicação MQTT

O backend recebe mensagens através do tópico:

```
acquaceg/devices/{device_id}/sensors/raw
```

Exemplo de payload:

```json
{
    "temperature": 25.4,
    "adc_ph": 790,
    "adc_condut": 450,
    "water_level": true
}
```

Campos:

| Campo | Descrição |
|-|-|
| temperature | Temperatura medida |
| adc_ph | Valor ADC do sensor de pH |
| adc_condut | Valor ADC da condutividade |
| water_level | Estado do nível de água |

---

# Banco de Dados

O backend utiliza PostgreSQL para armazenamento das leituras.

Tabela principal:

## sensor_readings

| Campo | Descrição |
|-|-|
| id | Identificador da leitura |
| mac_address | Identificação do dispositivo |
| temperature | Temperatura |
| ph | Valor de pH |
| conductivity | Condutividade |
| water_level | Estado do nível |
| created_at | Data da leitura |

---

# API REST

A API disponibiliza os dados armazenados para aplicações cliente.

## Endpoints principais

| Método | Endpoint | Descrição |
|-|-|-|
| GET | `/` | Status do serviço |
| GET | `/api/sensors/latest` | Última leitura |
| GET | `/api/sensors/readings` | Histórico de leituras |
| GET | `/api/sensors/readings/{id}` | Buscar leitura específica |
| DELETE | `/api/sensors/readings/{id}` | Remover leitura |

A documentação interativa da API é disponibilizada pelo FastAPI:

```
/docs
```

---

# Configuração

As configurações são carregadas através de variáveis de ambiente.

Principais variáveis:

| Variável | Função |
|-|-|
| DATABASE_URL | Conexão PostgreSQL |
| MQTT_BROKER | Endereço do broker |
| MQTT_PORT | Porta MQTT |
| MQTT_TOPIC | Tópico utilizado |
| MQTT_USERNAME | Usuário MQTT |
| MQTT_PASSWORD | Senha MQTT |

---

# Execução Local

Criar ambiente virtual:

```bash
python -m venv .venv
```

Ativar ambiente:

```bash
.\.venv\Scripts\activate
```

Instalar dependências:

```bash
pip install -r requirements.txt
```

Executar:

```bash
uvicorn app.main:app --reload
```

---

# Testes

Os testes atuais validam principalmente:

- Inicialização da aplicação;
- Encerramento dos serviços;
- Integração entre componentes;
- Gerenciamento do ciclo de vida.

Executar:

```bash
python -m unittest discover -s tests
```

---

# Próximas Evoluções

Possíveis melhorias futuras:

- Implementação de migrações com Alembic;
- Autenticação e autorização;
- Melhorias de observabilidade;
- Conversão dos valores ADC para unidades físicas;
- Expansão dos testes;
- Monitoramento de dispositivos conectados.
