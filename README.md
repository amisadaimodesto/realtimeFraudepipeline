# 🚀 Real-Time Fraud Detection Pipeline (Kafka + PySpark Streaming + PostgreSQL + Tableau)

Este projeto implementa um pipeline de engenharia de dados ponta a ponta para detecção e monitoramento de transações fraudulentas em tempo real. O sistema simula um fluxo contínuo de dados financeiros, processa eventos com baixa latência, persiste os alertas de forma segura em um banco relacional e os expõe em um dashboard interativo.

## 🛠️ Stack Tecnológica
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Apache Spark](https://img.shields.io/badge/Apache,_Spark-E25A1C?style=for-the-badge&logo=apachespark&logoColor=white)
![Apache Kafka](https://img.shields.io/badge/Apache,_Kafka-000000?style=for-the-badge&logo=apachekafka&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/postgres-%23316192.svg?style=for-the-badge&logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![Tableau](https://img.shields.io/badge/Tableau-E97627?style=for-the-badge&logo=tableau&logoColor=white)
![Linux / Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)

## 🏗️ Arquitetura do Sistema

O fluxo de dados foi desenhado seguindo as melhores práticas de sistemas distribuídos e alta disponibilidade:

1. **Producer (Simulador Python):** Gera transações financeiras contínuas e injeta anomalias/fraudes de alto valor.
2. **Streaming & Ingestão (Apache Kafka):** Garante a entrega das mensagens de forma resiliente através de um broker distribuído (gerenciado via Docker com Zookeeper).
3. **Processamento (PySpark Structured Streaming):** Consome o stream do Kafka, decodifica o payload JSON baseado em um Schema rígido, aplica regras de filtragem em tempo real para capturar apenas anomalias e processa os dados via micro-batches.
4. **Armazenamento / Sink (PostgreSQL):** Persistência dos alertas de fraude através de uma conexão JDBC assíncrona, utilizando volumes permanentes no Docker para blindagem contra perda de dados.
5. **Visualização (Tableau):** Camada de Business Intelligence conectada diretamente ao banco, exibindo tabelas de auditoria, rankings de contas afetadas, volumetria temporal e distribuição geográfica dos ataques.

## 🧰 Tecnologias Utilizadas

* **Linguagem Principal:** Python 3.12
* **Processamento de Big Data:** Apache Spark / PySpark 3.4.1 (Structured Streaming)
* **Mensageria & Streaming:** Apache Kafka (Confluent Platform 7.4.0) & Zookeeper
* **Banco de Dados:** PostgreSQL 15 (com Persistência de Volume Local)
* **Ambiente & Infraestrutura:** Docker, Docker Compose, Ubuntu 24.04 (WSL 2)
* **Dataviz:** Tableau

## 🚀 Como Executar o Projeto

**1. Subir a Infraestrutura (Docker):**
```
docker compose up -d
```
**2. Iniciar o Motor do Spark Streaming:**
```
source venv/bin/activate
python spark_streaming_processor.py
```
**3. Disparar o Simulador de Transações:**
```
source venv/bin/activate
python producer_simulator.py
```
**4. Conectar o Tableau**
```
Apontar o conector PostgreSQL para localhost:5432, banco fraud_db, usuário postgres e senha password123.
```
