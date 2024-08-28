# CDC with Debezium, Kafka, Postgres, Docker 

## Overview

A financial services company wants to improve its fraud detection capabilities by implementing a real-time monitoring system for financial transactions. The company processes a large number of transactions daily, including credit card purchases, wire transfers, and online payments. To detect fraudulent activities efficiently, they need a solution that can capture, process, and analyze these transactions as they occur.

## Objective
In this project, the main objective is to Implement a real-time data pipeline that captures every transaction change in the PostgreSQL database, streams it to Kafka, and uses a machine learning model or rule-based engine to analyze the transactions for potential fraud.

## Prerequisites

Before running this script, ensure you have the following installed:
- Python 3.9+
- `psycopg2` library for Python
- `faker` library for Python
- PostgreSQL server running locally or accessible remotely
- Docker and Docker Compose installed on your machine.
- Basic understanding of Docker, Kafka, and Postgres.

## Components
- PostgreSQL stores all financial transactions in a table. Each transaction includes details like transaction ID, amount, timestamp, account ID, merchant, and location.
- Debezium: Used to monitor changes in the PostgreSQL database. It captures every insert, update, or delete operation in the transactions table and streams these changes to Kafka.
- Kafka Producer: Acts as a distributed messaging system that receives the transaction data from Debezium and makes it available to multiple consumers in real time.
- Docker: Used to containerize all services, ensuring a consistent and easily deployable environment.
- Kafka Consumers: A microservice (Python) that consumes the transaction stream from Kafka, applies machine learning models or rule-based checks to identify suspicious activities, and flags potential fraud.
- Dashboard Service: A real-time dashboard that visualizes the transaction flow and alerts on detected fraud.


## Installation

1. **Install Required Python Libraries:**

   You can install the required libraries using pip:

   ```bash
   pip install psycopg2-binary faker
   ```

## Services in the Compose File

- **Zookeeper:** A centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services.
- **Kafka Broker:** A distributed streaming platform that is used here for handling real-time data feeds.
- **Confluent Control Center:** A web-based tool for managing and monitoring Apache Kafka.
- **Debezium:** An open-source distributed platform for change data capture.
- **Debezium UI:** A user interface for managing and monitoring Debezium connectors.
- **Postgres:** An open-source relational database.

## Implementation Steps
- Setup the CDC Environment: Use Docker Compose to set up Zookeeper, Kafka, Debezium, and PostgreSQL services.
Start the services by running
 ```bash
docker-compose up -d
 ```

- Configure Debezium Connector: Configure a Debezium PostgreSQL connector to monitor the transactions table. The connector will capture all data changes and stream them to Kafka in real time.

- Develop and Deploy Kafka Consumers: Build the Fraud Detection Service that consumes Kafka topics for transaction data, applies fraud detection logic, and alerts on any suspicious activity.
- Deploy a Dashboard Service that consumes data and provides a real-time visualization of transaction flow and fraud alerts.

Monitor and Manage Services: Use Kafka Control Center and Debezium UI to monitor data streams and connectors. Scale services up or down based on transaction volume.

**Verify the Services:**
   Check if all the services are up and running:

   ```bash
   docker-compose ps
   ```

   You should see all services listed as 'running'.

5. **Accessing the Services:**
   - Kafka Control Center is accessible at `http://localhost:9021`.
   - Debezium UI is accessible at `http://localhost:8080`.
   - Postgres is accessible on the default port `5432`.

6. **Shutting Down:**
   To stop and remove the containers, networks, and volumes, run:

   ```bash
   docker-compose down
   ```

## Customization
You can modify the Docker Compose file to suit your needs. For example, you might want to persist data in Postgres by adding a volume for the Postgres service. This setup is intended for development and testing purposes. For production environments, consider additional factors like security, scalability, and data persistence.
