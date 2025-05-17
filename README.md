# 🦟 Dengue Data ETL Platform

本專案透過 Apache Airflow 自動化取得台灣登革熱疫情資料，並進行清洗與後續資料分析。

## ✅ 功能模組
- 使用 CDC API 抓取每日登革熱統計資料
- Airflow DAG 控制下載與清理流程
- 清理後資料儲存於本地 CSV（未來支援 BigQuery）
- MCP 架構規劃：n8n → Airflow → 清洗 → BigQuery → Looker Studio

## 📁 資料夾結構
```
.
├── dags/
│   └── etl_dengue_stats_dag.py
├── data/
├── scripts/
│   └── clean_data.py
├── README.md
└── docker-compose.yaml（若使用 Airflow 官方範本）
```

## 📅 專案時程
- Week 1：環境建置與資料清洗 ✅
- Week 2：ETL 上雲 + n8n 整合（進行中）
- Week 3：視覺化與洞察產出（預定）

## 📊 數據來源
- [CDC 登革熱 API](https://data.cdc.gov.tw/dataset/7c9245d0-8a53-4663-8ea5-4f1c8ed6a760)

---
由 Vanessa 製作 👩‍💻