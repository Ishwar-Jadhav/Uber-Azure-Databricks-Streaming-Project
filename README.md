# Uber-Azure-Databricks-Streaming-Project
Data Engineering Project built using Databricks, Azure Data Factory, Azure Event Hubs, PySpark, Spark Structured Streaming, and Spark Declarative Pipelines.

## Architecture diagrams explained

### 1. Web application to Azure Event Hub
A web application captures user “book ride” actions and sends them to an Azure Function. The function publishes these as events into Azure Event Hub using secure keys, turning front‑end interactions into scalable, cloud‑native event streams that downstream consumers can process independently.

<img width="2940" height="1912" alt="Image 3-1-26 at 16 19" src="https://github.com/user-attachments/assets/e8b44b2b-34e0-4b1e-ae85-a26205402e3b" />

