# Change Data Capture (CDC) with Debezium & Kafka

## Overview
A real-time CDC pipeline that captures database changes from PostgreSQL, streams them through Kafka, and materializes them as Parquet files in a data lake. The pattern every modern data platform uses to sync operational and analytical systems.

## Architecture
- **Source**: PostgreSQL with logical replication enabled
- **CDC Engine**: Debezium PostgreSQL connector capturing WAL changes
- **Streaming**: Kafka (or Redpanda) as the event backbone — one topic per table
- **Consumer**: Python consumer (confluent-kafka) that deserializes Avro/JSON events, applies transformations, and writes Parquet files partitioned by date
- **Data Lake**: MinIO (S3-compatible) with Parquet files organized by table/date
- **Monitoring**: Kafka lag monitoring, Debezium connector health checks via Airflow sensors

## Tech Stack
- PostgreSQL 15 (source database)
- Debezium 2.x (CDC connector)
- Apache Kafka / Redpanda
- Python 3.11+, confluent-kafka, PyArrow
- MinIO / AWS S3
- Apache Airflow 2.x (monitoring & alerting)
- Docker & Docker Compose

## What This Demonstrates
- Change Data Capture architecture and implementation
- Kafka/event streaming fundamentals
- Debezium connector configuration and monitoring
- Parquet file writing with partitioning strategies
- Real-time data lake ingestion patterns

## Status
🚧 In Development

## Project Structure
├── debezium/
│   └── connector-config.json
├── kafka/
│   └── docker-compose.kafka.yml
├── consumer/
│   ├── cdc_consumer.py
│   └── writers/
├── dags/
│   └── cdc_monitoring_dag.py
├── sql/
│   └── source_schema.sql
├── tests/
├── docker-compose.yml
└── README.md
