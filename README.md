<<<<<<< HEAD
<<<<<<< HEAD
# nhi-data-platform
=======
# 健保資料自動分析與可視化平台（含 MCP 架構）
=======
## 健保資料自動分析與可視化平台（含 MCP 架構）
>>>>>>> 063d859 (更新 README 說明內容)

> 本專案為以 GCP 為基礎，整合 Apache Airflow、n8n、BigQuery 與 Looker Studio 的健保資料自動分析平台。並進一步導入 MCP（Model–Context–Protocol）架構，強化生成式 AI 對資料的摘要與解釋能力。

---

## 🔍 專案簡介

本平台旨在自動化收集並分析台灣健保署重大用藥公開資料，實作資料工程與生成式 AI 的結合。資料流設計如下：

* 使用 **n8n** 管理資料觸發與通知流程
* 使用 **Airflow DAG** 管理 ETL 任務與清洗邏輯
* 使用 **BigQuery** 作為雲端資料倉儲
* 使用 **Looker Studio** 建立互動式儀表板
* 使用 **OpenAI GPT 模型** 擴充報表的自動摘要與趨勢解釋

---

## 🛠️ 使用技術

* Python（pandas、requests）
* Apache Airflow
* n8n（Webhook & Task Control）
* Google Cloud Platform（BigQuery、IAM、Service Account）
* Looker Studio
* OpenAI GPT API（AI 摘要與自動解釋）
* Prompt Engineering（for MCP Protocol）

---

## 🧱 系統架構與 MCP 應用

### 專案背景與目標

隨著醫療數據量的迅速增長，如何有效地整合、分析與解釋這些數據，成為當前醫療產業亟待解決的挑戰。本專案旨在開發一個基於 Google Cloud Platform (GCP) 的健保資料自動分析平台，整合 Apache Airflow、n8n、BigQuery 和 Looker Studio，並進一步導入 Model-Context-Protocol (MCP) 架構，結合生成式 AI 進行資料的摘要與解釋，實現更加智能化、高效化的健保資料分析與報告生成。

### 系統設計與技術整合

平台的資料流程如下：

```
[ n8n webhook ] → [ Airflow DAG (ETL) ] → [ BigQuery Table ] → [ Looker Dashboard ]
                                                    ↓
                                                [ Context 摘要 ]
                                                    ↓
                                              [ GPT 模型摘要 ]
```

* **Apache Airflow**：作為主要的資料流管理工具，負責定期抓取健保資料、清理與轉換，並寫入 BigQuery。
* **n8n**：負責 webhook 觸發與資料流啟動，並負責報表完成後的通知流程。
* **BigQuery**：作為資料倉儲，提供高效分析查詢能力。
* **Looker Studio**：視覺化呈現用藥趨勢與分析報表。
* **OpenAI GPT API**：處理 Looker 匯出的摘要資料，產出自然語言報告。

### MCP 架構應用詳述

| MCP 組件       | 對應功能                         | 實作方式                                         |
| ------------ | ---------------------------- | -------------------------------------------- |
| **Model**    | 使用 OpenAI GPT-4 對報表進行摘要、洞察生成 | 調用 GPT API，使用自訂 Prompt                       |
| **Context**  | 來自 BigQuery 的摘要資料，如：年度用藥總量變化 | pandas 處理後餵入 GPT                             |
| **Protocol** | 統一的 Prompt 模板，標準 JSON 結構傳輸   | 自訂格式，如 `{ context: "...", prompt: "請生成摘要" }` |

#### MCP 實例：

```json
{
  "context": "根據 2024 年 Q1 資料，抗生素類用藥顯著上升，特別在北部地區增加 27%。整體用藥支出提高 8%。",
  "prompt": "請針對以上資料生成 150 字的趨勢摘要，語氣正式，便於主管理解。"
}
```

GPT 回應範例：

> 「2024 年第一季，抗生素使用量大幅上升，尤以北部地區為主，成長率達 27%。同時整體用藥支出增加 8%，可能與流感季節提前相關。」

### 📌 應用場景與價值

* **精準醫療與健康管理**：根據用藥資料預測高風險族群，結合 GPT 模型快速產出行動建議。
* **醫療資源優化**：系統自動分析各地區用藥趨勢，並推播給管理人員。
* **醫療費用控制**：自動預測支出異常，並用 AI 模型生成建議。
* **個性化報表摘要**：依不同角色（主管／醫師）生成不同語氣、重點的報告摘要。

---

## 📅 開發進度（截至 2025/5/13）

| 任務              | 狀態 |
| --------------- | -- |
| GitHub Repo 初始化 | ⬜  |
| 資料來源確認          | ⬜  |
| Airflow 安裝完成    | ✅  |
| n8n webhook 測試  | ⬜  |
| BigQuery 建表     | ⬜  |
| Looker 報表設計     | ⬜  |
| GPT 摘要流程測試      | ⬜  |

---

## 👩‍💻 作者

| 姓名      | 角色        | 技術                                        |
| ------- | --------- | ----------------------------------------- |
| Vanessa | 專案主導／資料工程 | Airflow, GCP, GPT API, Data Visualization |

---

## 📄 License

MIT License
>>>>>>> 920bc73 (Add README with MCP structure)
