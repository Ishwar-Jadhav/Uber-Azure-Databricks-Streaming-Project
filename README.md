# Uber-Azure-Databricks-Streaming-Project
Data Engineering Project built using Databricks, Azure Data Factory, Azure Event Hubs, PySpark, Spark Structured Streaming, and Spark Declarative Pipelines.

## Architecture diagrams explained

<img width="2940" height="1912" alt="Image 3-1-26 at 16 19" src="https://github.com/user-attachments/assets/e8b44b2b-34e0-4b1e-ae85-a26205402e3b" />

### 1. Web application to Azure Event Hub
A web application captures user “book ride” actions and sends them to an Azure Function. The function publishes these as events into Azure Event Hub using secure keys, turning front‑end interactions into scalable, cloud‑native event streams that downstream consumers can process independently.

<img width="796" height="811" alt="1" src="https://github.com/user-attachments/assets/25b8a407-fa03-4a1d-9a9d-464910374d71" />

### 2. Azure Event Hub – Pub/Sub and producer–consumer
Azure Event Hub implements the pub/sub and producer–consumer patterns for ride events. The web app acts as a producer publishing Event1, Event2, etc., into Event Hub with a defined retention/expiry window, while Databricks acts as a consumer that reads and processes these events without being tightly coupled to the producers.

<img width="772" height="592" alt="2" src="https://github.com/user-attachments/assets/7a2760f1-c371-4356-9372-07002d1192d4" />

### 3. Azure Data Factory to Data Lake
Azure Data Factory orchestrates ingestion pipelines that pull data or configuration from GitHub and land it in ADLS Gen2. This creates the raw/bronze storage in the data lake, which acts as the single source of truth for Databricks jobs that build the silver and gold layers.

<img width="735" height="512" alt="3" src="https://github.com/user-attachments/assets/ff9a9878-2932-420c-9147-0931048779b4" />

### 4. Ingestion into Databricks – Events and files
The project uses two main ingestion paths into Databricks. Real‑time events are read directly from Azure Event Hub for streaming analytics, while batch data is loaded from ADLS Gen2 so that historical files and live streams can be processed together in the same platform.

<img width="782" height="816" alt="4" src="https://github.com/user-attachments/assets/6bd5e9f9-39e5-482c-aa58-2e57622ab1bb" />

### 5. Silver layer – Unifying batch and streaming
The silver layer combines historical (initial load) and real‑time (stream) data. Initial load and streaming inputs are unified into a single streaming table, then joined (using Jinja‑driven logic) to produce a curated OBT that feeds the gold layer, ensuring both past and live rides are available for analysis.

<img width="915" height="761" alt="5" src="https://github.com/user-attachments/assets/ecf21f63-cf79-4cfd-bd20-ecaaafe1ec6b" />

### 6. Gold layer – Star schema and OBT
The gold layer contains business‑ready tables modeled as a star schema, with a central fact table joined to Location, Payment, Booking, Passenger, and Vehicle dimensions. An additional OBT (One Big Table) is built on top to simplify analytics and dashboard queries by denormalizing the most commonly used attributes.

<img width="1121" height="632" alt="6" src="https://github.com/user-attachments/assets/a9283eca-dad2-4114-b7cc-c715b77d7838" />


