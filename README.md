# Dengue Data ETL Platform

本專案整合 Apache Airflow 自動化取得台灣登革熱疫情資料，並進行清洗、雲端儲存與視覺化分析，同時搭配 LINE 聊天助理與報表推播服務。

---

## 專案簡介

本專案透過 LINE Chatbot + n8n + Google Gemini + BigQuery + Streamlit + Metabase，實現使用者輸入地區與月份，自動回覆登革熱統計報表，支援互動式視覺化與 LINE 即時回應。

---

## 使用技術（Tech Stack）
- Python：資料清理與 EDA
- Airflow (Docker)：定時抓取與轉換任務排程
- n8n + LINE Bot：聊天機器人回覆與查詢互動流程
- Google Gemini：自然語言解析地區與月份
- BigQuery：儲存與查詢處理後的病例數據
- Metabase / Looker Studio：互動式趨勢報表
- Streamlit：圖表視覺化與報表頁面產生
- Render / GitHub / Notion：部署與文件整合

---

## 架構與資料流程

```
n8n → Gemini AI → BigQuery → Streamlit / Metabase → LINE 回傳
             ↓
       Airflow → CDC API → 資料清洗 → 上傳 BigQuery
```

---

## 功能模組
- 使用 CDC API 抓取每日登革熱統計資料
- Airflow DAG 控制下載與清理流程
- 清理後資料儲存於 BigQuery（支援 CSV 與月報彙整）
- 使用者輸入「查詢 台南 5 月」即可查詢即時統計結果
- 報表可透過 Streamlit 或 Metabase 視覺化頁面查看

---

## 資料夾結構
```
.
├── .ipynb_checkpoints/
├── config/
├── credentials/
├── dags/
│   └── etl_dengue_stats_dag.py
├── data/
├── docs/
├── logs/
├── n8n/
├── n8n-fly/
├── plugins/
├── reports/
├── scripts/
│   └── clean_data.py
├── sqlite/
├── .env
├── .gitignore
├── docker-compose.yaml
├── Dockerfile
└── README.md
```

---

## 模組與資料表命名
- `daily_cases`：每日病例明細
- `monthly_cases`：月份統計表
- `city_cases`：各縣市統計
- `gender_age_cases`：性別與年齡層彙總
- `summary_report`：整合查詢報表（供 Streamlit / LINE 使用）

---

## 專案時程（初步）
- Week 1：Airflow + Python 環境建置與資料清洗 ✅
- Week 2：ETL 上雲 + n8n 整合 + LINE 串接 ✅
- Week 3：視覺化與使用者查詢互動 ✅
- Week 4：Metabase + 報表設計與部署（進行中）

---

## 數據來源
- [CDC 登革熱開放資料](https://data.cdc.gov.tw/dataset/7c9245d0-8a53-4663-8ea5-4f1c8ed6a760)

---

## 使用者操作流程
1. 使用者輸入：「查詢 台南 5 月」
2. n8n 呼叫 Gemini 解析輸入意圖
3. Structured Output Parser 輸出地區與時間 → 驗證
4. 產生 BigQuery SQL 並查詢登革熱資料
5. 由 LINE Bot 回傳：圖表頁面 / 統計摘要 / 查詢錯誤提示

---

## 心得收穫
- 練習 Gemini Prompt 設計與結構化輸出控制
- 熟悉 BigQuery SQL 查詢、n8n 的 webhook + 分流邏輯
- 自動化平台整合經驗大幅提升部署與除錯能力

---

## 挑戰與解法（Challenges & Solutions）

| 挑戰問題 | 解法 |
|----------|------|
| Gemini 輸出錯誤 JSON | 加入 Safe JSON Parser 判斷與 try catch |
| 無效輸入無法提示 | 透過 is_valid 判斷 + LINE 預設錯誤回應 |
| LINE Push 限制 | 改用 Reply Token 解決未驗證帳號推播問題 |
| Airflow Docker 建置困難 | 採用官方 airflow-composer 並調整 Volume 權限 |
| BigQuery 權限不足 | IAM 設定為 BigQuery Admin 並確認 dataset 權限 |
| Looker Studio 報表限制 | 採用 summary table 簡化欄位並設參數綁定 |
| Python 圖表無法顯示中文字 | 手動設定字型與 rcParams 解決亂碼 |

---

由 Vanessa 製作

