# 🧮 OTIF Dashboard — Supplier and Delivery Performance Analysis

This project contains two PostgreSQL queries used to build widgets for an **OTIF (On-Time In-Full) dashboard**, which helps monitor supplier performance and delivery accuracy across clients and distribution centers.

Both queries are based on the same core logic for determining:
- Whether a delivery was **on time or late**
- Who is responsible for the delay (**supplier, distribution center, or both**)
- How **client-specific delivery windows** affect the final assessment

---

## 🛠️ Features

- **Unified Logic for Delay Detection**:  
  Uses `client_delivery_date`, `date_delivery`, and `timegate` to calculate delays with client-specific grace periods.

- **Supplier vs Distribution Center Accountability**:  
  Classifies responsibility using complex `CASE WHEN` conditions based on shipment timestamps.

- **Client-Specific Grace Periods**:  
  Client #2 gets a **7-day grace period**, which affects how delays are classified.

- **Two Views for One Dashboard**:
  - Query 1: Aggregates total GMV and model count by delivery status.
  - Query 2: Splits metrics into **on-time vs late**, and adds **distribution center names** for deeper insight.

---

## 📌 Key Metrics

| Metric | Description |
|--------|-------------|
| `"Факт опоздания"` | Status of delivery: 'Вовремя', 'Опоздало, приехало', 'Опоздало, в пути' |
| `gmv_intime` / `gmv_late` | GMV split by delivery timing |
| `model_count_intime` / `model_count_late` | Number of models delivered on time vs late |
| `who` | Responsible party: 'Поставщик', 'РЦ', 'Задержка приемки РЦ', etc. |
| `EXorCYEK` | Grouping by enterprise group (ЕХ / СУЭК) |

---

## 📊 Business Use Cases

This dashboard supports supply chain and procurement teams in answering key questions like:

- Which suppliers are most frequently late?
- Are there distribution centers causing repeated delays?
- How often do we meet delivery deadlines across different clients?
- Which orders were partially delayed?

---


## 🔍 Core Logic Shared Between Queries

All key parts — including `full_delivery`, `who`, and `timegate` CTEs — are **identical across both files**, ensuring consistent results between widgets.

The only difference lies in the final aggregation layer (`fact` CTE), where one query gives totals and the other breaks them down further.

---

## 🚀 Why This Matters

This kind of analysis is critical in **B2B logistics and procurement**, where timely deliveries directly impact customer satisfaction and internal efficiency.

Having **two views built from the same logic** ensures **data consistency** and makes it easier to maintain and scale the dashboard over time.

---

## 🖥️ Sample Output

## Code#1.1 - 1.2 - Business requirement - demonstration of a full dynamics

![image](https://github.com/user-attachments/assets/e4728636-7bd3-4096-9037-9df0b80a0fdc)


## Code#2.1 - 2.2 - Business requirement - demonstration of a full map

![image](https://github.com/user-attachments/assets/c2fea9e2-a77a-4683-8eef-c5763aaf97bb)

