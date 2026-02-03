# 🌦️ Real-Time Weather Data Pipeline: Kafka to Microsoft Fabric

This project implements an end-to-end real-time data engineering pipeline. It captures live weather data from an API, streams it through a local **Apache Kafka** cluster, and processes it in the cloud using **Microsoft Fabric (PySpark)** for time-windowed analytics.

---

## 🏗️ System Architecture

The pipeline follows these stages:
1. **Source:** Live weather data from Amsterdam (OpenWeatherMap API).
2. **Ingestion:** Python-based Kafka Producer.
3. **Broker:** Apache Kafka & Zookeeper running on **Docker**.
4. **Bridge:** **Ngrok** tunnel to securely expose the local Kafka broker to the internet.
5. **Processing:** **PySpark Structured Streaming** on Microsoft Fabric.
6. **Sink:** Delta Table in a Fabric Lakehouse.

---

## 🚀 Implementation Steps

### 1. Infrastructure (Docker & Kafka)
The environment is containerized using Docker. It includes Zookeeper for coordination, Kafka as the message broker, and Kafka-UI for visual monitoring.

<img width="1606" height="969" alt="2 docker" src="https://github.com/user-attachments/assets/4e5056c2-4fd2-4c00-b72a-dd7eff951e93" />
*Figure 1: Docker Desktop managing the Kafka ecosystem.*

### 2. Live Data Production
The `weather_producer.py` script fetches data every few seconds and sends it to the `weather_data` topic. A local consumer verifies the flow.

<img width="1919" height="1079" alt="1 kod" src="https://github.com/user-attachments/assets/156e7d13-bd42-4662-90ca-af9ea32ab547" />
*Figure 2: Active terminals showing the Ngrok tunnel, Producer, and Consumer.*

### 3. Topic Monitoring
Using **Kafka-UI**, we can inspect the raw JSON messages to ensure the schema and timestamps are correct before they reach the cloud.

<img width="1919" height="1079" alt="3 ui for apache kafka" src="https://github.com/user-attachments/assets/75e8f213-4339-4499-a258-33ebf372f184" />
*Figure 3: Kafka-UI showing live message offsets and payloads.*

### 4. Real-Time Analytics (Fabric & Spark)
In Microsoft Fabric, we use a **Sliding Window** aggregation. The system calculates the average temperature for **5-minute windows**, updating every **1 minute**.

### 5. Final Storage (Delta Table)
The processed data is saved as a **Delta Table** in the Lakehouse, providing a structured historical record for reporting.

<img width="1919" height="1079" alt="4 fabric" src="https://github.com/user-attachments/assets/6d847a27-96c2-4afd-a6a7-5f09852cd673" />
*Figure 4: The final avg_temperature table in Microsoft Fabric.*

---

## 🛠️ Tech Stack

| Component | Technology |
| :--- | :--- |
| **Language** | Python, PySpark |
| **Streaming** | Apache Kafka |
| **Containerization** | Docker |
| **Cloud Platform** | Microsoft Fabric |
| **Connectivity** | Ngrok |
| **Table Format** | Delta Lake |

---
