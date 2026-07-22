<div style="display:flex;justify-content:space-between;align-items:baseline;margin-bottom:20px">
<a href="../README.md">← 返回所有職缺</a>
<a href="../../roles/ai-data-engineer.md">English</a>
</div>

# AI Data Engineer

## 30 秒認識 Mlytics

Mlytics 是一套 AI Answer Engine。我們幫媒體與出版業者把讀者意圖轉化為商業成果——用高品質的 CPL 收入，取代持續下滑的 CPM 收入。我們的 Intent Refinery 已在 15+ 家台灣頭部媒體上線，服務 4M+ 週活躍使用者。

我們從 multi-CDN 起家。那套基礎設施——<50ms 路由、multi-vendor failover——現在是整個產品的技術底層。

[更認識 Mlytics →](../README.md)

---

## 這個角色

你會加入 **Data & Innovation 團隊**，向我們的 Data & Innovation Lead Tim 匯報。Tim 已經把地基打好：Databricks 搭配 Unity Catalog、CDN 使用資料的 medallion architecture、用 MLflow 做實驗追蹤、為 AIGC 產品建置 vector search 與 embedding pipeline。架構選型都已定案，缺的是那個把意圖資料規格變成 production 系統的人。

這不是研究型職位。我們已經設計好行為追蹤 pipeline（Bronze → Silver → Gold）、定義了 6 個複合意圖訊號分層與各自的 CPC 定價、建好意圖分類（taxonomy）框架，也把 second-price auction 媒合引擎的規格寫好了。規格已經存在。**你的工作是把它們變成真的**——然後根據資料實際告訴你的事，把它們做得更好。

你會和全端產品工程師（負責 widget 與 API 層）、Tim（ML 實驗與模型選型）密切合作，並直接和 Head of Product 及 CEO 討論資料在商業上的意義。當 BD 團隊走進一家金融品牌的會議，說「我們可以告訴你哪些使用者正在認真考慮退休規劃、哪些只是隨手瀏覽」——這句話背後的底氣，來自你的 pipeline。

---

## 前 90 天你會做什麼

**第 1 個月 — 把行為追蹤 pipeline 上線。**

我們的 clickstream SDK 從 58 個媒體網站捕捉 8 種 event（page_enter、scroll_depth、active_time、page_exit、widget_visible、qa_click、qa_read、cross_page），資料以 JSON 落在 S3。你的第一個交付物，是 Databricks 上的 production pipeline：

- **Bronze：** 用 Auto Loader 從 S3 串流攝取進 raw Delta table
- **Silver：** 解析、驗證、GeoIP 加值後的 event 記錄，並做 session stitching
- **Gold：** 每小時的 session_summary 聚合——engagement 分層、scroll 深度、active time、Q&A 互動深度、search intent 訊號

到第 1 個月結束，pipeline 已上線、被監控，並以 <5 分鐘的端到端延遲處理全部 58 家媒體的 event。

**第 2 個月 — 實作意圖評分，並讓它可被查詢。**

session_summary 這張 Gold table 會餵進一個複合意圖評分模型，把使用者分成商業價值差異極大的分層：

- **Deep Reader + Decision Click** → CPC $1.50–$2.00（active >60s、scroll >75%、點擊了決策階段的 Q&A）
- **Search Intent + Q&A Engagement** → CPC $1.50–$2.00（search referrer + 2 次以上 Q&A 點擊 + >10s 閱讀時間）
- **Multi-Article Researcher** → CPC $1.00–$1.50（3 頁以上、active >3 分鐘）
- 一直到 **Bounce** → 不變現（<10s、scroll <25%、0 點擊）

在這之上建一個 Genie Room，讓商業團隊能自助查詢：「給我這週 cnyes.com 上投資垂直領域的高意圖使用者」應該在幾秒內回答，而不是要開一張 data team 的工單。

**第 3 個月 — 打造媒合引擎的基礎。**

把意圖訊號連到廣告主的 campaign。實作核心媒合邏輯：intent classification → campaign filter（vertical、publisher、intent L1/L2/L3）→ score（bid × confidence × profile richness × 歷史 CTR）→ second-price auction。這裡就是你的 pipeline 與全端工程師的 Sponsored Questions 產品交會之處——Intent Refinery 第一個產生營收的整合。

---

## 我們在找的人

**不可妥協的條件：**

- 你建過商業團隊真的會依賴的 production 資料 pipeline——不是只跑一次的 notebook。串流攝取、轉換、聚合、監控、告警。
- 你在 production 規模上精通 **Python 與 SQL**。你寫過 Spark job，不是只有 pandas 腳本。
- 你有 **Databricks** 或同級 lakehouse 平台（Delta Lake、Unity Catalog、Structured Streaming）的實作經驗。你懂 medallion architecture，也懂為什麼 governance 很重要。
- 你能實作 ML 評分模型並把它部署成 production 功能——而不是丟給「工程團隊」。你把模型 operationalize 成持續運行的東西，而不是只在 notebook 裡訓練出來就停。
- 你把資料當成一個**產品**，而不是倉庫。你在意延遲、新鮮度、準確度，以及下游消費者（人或 API）能不能真的用你產出的東西。

**會讓你脫穎而出的加分：**

- 曾在 ad tech、martech 或 fintech 建過**即時使用者評分或分群系統**——你看過 production 上「意圖訊號」長什麼樣，也分得出有用的訊號和雜訊。
- 熟悉 **MLflow** 的實驗追蹤與模型管理——Tim 大量使用它，你會和他一起做模型選型與 A/B 測試。
- 有 **vector search 與 embedding** 用於內容或使用者相似度的經驗——這會餵進跨站意圖輪廓與 content-to-intent 媒合。
- 你建過資料品質直接決定營收的系統——定價引擎、推薦系統、詐欺評分或廣告競價機制。
- 中文溝通能力 — 我們團隊日常混用中英文，如果你能用中文討論技術方案和數據定義，會是很大的加分。

---

## 技術棧

| 層 | 我們用什麼 |
|-------|-------------|
| Platform | Databricks / Unity Catalog / Delta Lake |
| Compute | Spark Structured Streaming / Databricks Workflows |
| ML | MLflow / Python / embeddings / vector search |
| Storage | S3（clickstream）/ PostgreSQL / Redis |
| Languages | Python / SQL / 部分 Go 用於服務整合 |
| Infra | GCP / AWS / CloudFlare Workers（收集端點）|
| Observability | Databricks SQL dashboards / Grafana / alerting |

---

## 這個角色如何連到更大的全局

Intent Refinery 有四個變現層。你的 pipeline 驅動全部四層：

| 產品 | 定價 | 你的資料如何讓它成立 |
|---------|---------|---------------------------|
| Sponsored Questions | CPC $0.50–$2.00 | intent classification 觸發即時廣告競價 |
| Intent Display Network | CPM $15–$40 | 使用者意圖輪廓讓 premium targeting 成為可能 |
| Intent Micro-sites | CPL $5–$20 | 跨站意圖圖譜辨識出高價值 lead |
| Full Conversation | Performance | 多輪對話評分決定轉換成熟度 |

第 6 個月的商業目標是 $70–100K+ MRR。全端工程師建的功能是表層。**你的 pipeline 是底下那具引擎。**

---

## 為什麼是現在

我們正在募下一輪。投資論點是：在內容消費當下捕捉到的即時意圖資料，在結構上比歷史行為資料或情境式投放更有價值。而這個論點，只會和證明它的資料系統一樣強。

現在，一個品牌潛在客戶問「這跟 contextual advertising 有什麼不同？」，我們拿出一份規格給他看。等你 ship 之後，我們給他看的是一個 live dashboard：一個 Deep Reader + Decision Click 使用者值 $1.50 CPC，一個 Casual Browser 值 $5 CPM——30 倍的價差。這就是「假設」和「生意」的差別。

---

**想看看我們實際上怎麼打造這些？** → [我們怎麼做事：Becoming Product Builders with Business Thinking](../../how-we-ship.md)

---

## 如何應徵

寄給我們任何能展現你怎麼思考資料系統的東西——你建過的 pipeline、你做過的一個架構決策與原因、你 operationalize 過的評分模型。我們在意的是你 ship 過什麼，不是你用過哪些工具。

📧 **[career@mlytics.com](mailto:career@mlytics.com)**
