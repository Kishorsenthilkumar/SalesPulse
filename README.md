# Real-Time & Batch Data Processing Pipeline  

This project demonstrates a **modern data engineering pipeline** that integrates real-time and batch data sources, processes them using streaming and batch frameworks, and stores curated results for downstream analytics and reporting.  

The architecture follows the **Bronze → Silver → Gold** data layering approach, ensuring scalability, flexibility, and reliability.  

---

## 🚀 Architecture Overview  

```mermaid
flowchart TD
    A[Data Generator - POS, etc.] --> B1[Kafka - Sales Events]
    A --> B2[Airflow DAGs - Batch Sources]

    B1 --> C1[Kafka → MinIO Bronze (Stream Bucket)]
    B2 --> C2[Batch Data → MinIO Bronze (Batch Bucket)]

    C1 --> D1[Flink - Real-time Transformation]
    C2 --> D2[Spark - Batch Transformation]

    D1 --> E1[Postgres - Real-time Results]
    D2 --> E2[Postgres - Batch Results]

    E1 --> F1[dbt - Data Quality Checks]
    E2 --> F2[dbt - Data Marts]
```

---

## 🔄 Process Flow  

1. **Data Generation**  
   - Synthetic data is generated (e.g., **POS system events**).  

2. **Data Ingestion**  
   - **2.1** POS sales events are streamed into **Kafka topics**.  
   - **2.2** Batch data is collected from external sources via **Airflow DAGs**.  

3. **Bronze Layer (Raw Storage)**  
   - **3.2** Kafka events are written in parallel to **MinIO stream bucket**.  
   - **3.3** Batch data is written to **MinIO batch bucket**.  

4. **Processing**  
   - **4.1** **Spark** performs **batch transformation & analysis**.  
   - **4.2** **Flink** performs **real-time transformations** (enrichment, aggregation, filtering, alerts).  

5. **Serving Layer (Postgres)**  
   - **5.1** Flink results are stored in **Postgres**.  
   - **5.2** Spark results are stored in **Postgres**.  

6. **Analytics & Quality**  
   - **6.1** **dbt** validates **data quality checks**.  
   - **6.2** **dbt** builds **data marts** for BI dashboards & analytics.  

---

## 🧑‍🤝‍🧑 Who Can See Which Processes?  

- **Data Engineers** → Processes **1, 2.1, 2.2, 3.2, 3.3, 4.1, 4.2**  
- **Streaming Engineers** → Processes **2.1, 3.2, 4.2, 5.1**  
- **Batch Engineers** → Processes **2.2, 3.3, 4.1, 5.2**  
- **Database Engineers** → Processes **5.1, 5.2, 6.1, 6.2**  
- **Analytics/BI Teams** → Processes **6.1, 6.2**  

---

## 🛠️ Tech Stack  

- **Data Ingestion:** Kafka, Airflow  
- **Storage:** MinIO (Bronze Layer)  
- **Processing:** Spark (Batch), Flink (Streaming)  
- **Serving:** Postgres  
- **Transformation & Quality:** dbt  
- **Orchestration & Monitoring:** Airflow, Kafka Connect  

---

## 📂 Project Structure  

```
├── airflow/             # DAGs for batch ingestion
├── kafka/               # Kafka setup & topics
├── flink/               # Flink jobs (real-time)
├── spark/               # Spark jobs (batch processing)
├── dbt/                 # dbt models, tests, and marts
├── minio/               # Storage buckets (bronze layer)
└── docs/                # Architecture diagrams & notes
```

---

## 📊 Use Cases  

- **Real-time sales monitoring** (alerts, anomaly detection).  
- **Batch reporting & analytics** (daily/weekly trends).  
- **Data quality validation** before reporting.  
- **Unified data marts** for BI dashboards (Power BI, Tableau, Looker).  

---

## ✅ Next Steps  

- Add **CI/CD pipelines** for dbt models.  
- Deploy on **Docker / Kubernetes** for scalability.  
- Integrate with **BI tools** for visualization.  

---

📌 This repository serves as a **blueprint for hybrid batch + streaming pipelines** using open-source tools.  
