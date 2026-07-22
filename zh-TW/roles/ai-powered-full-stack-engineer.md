<div style="display:flex;justify-content:space-between;align-items:baseline;margin-bottom:20px">
<a href="../README.md">← 返回所有職缺</a>
<a href="../../roles/ai-powered-full-stack-engineer.md">English</a>
</div>

# Lead AI-Native Full Stack Engineer

## 30 秒認識 Mlytics

Mlytics 是一套 AI Answer Engine。我們幫媒體與出版業者把讀者意圖轉化為商業成果——用高品質的 CPL 收入，取代持續下滑的 CPM 收入。我們的 Intent Refinery 已在 15+ 家台灣頭部媒體上線，服務 4M+ 週活躍使用者。

我們從 multi-CDN 起家。那套基礎設施——<50ms 路由、multi-vendor failover——現在是整個產品的技術底層。

[更認識 Mlytics →](../README.md)

---

## 這個角色

你會是第一批專職投入 Intent Refinery 產品線的工程師之一，直接和 Head of Product 與 CEO 一起工作。這裡沒有 backlog 等你整理——有的是一個等著被閉合的營收迴圈，而你會有把它閉合的自主權。

「End-to-end」是字面上的意思。我們是一個不到 30 人的團隊，沒有 DevOps 團隊、沒有 SRE 團隊、沒有 platform 團隊。**你擁有你所打造之物的完整生命週期**——從 API 設計、前端體驗、部署、可觀測性，到凌晨兩點通知你某個東西壞掉的那個告警。這不是人力缺口，而是我們相信在這個階段軟體就該這樣被打造。如果你只待過「部署有別人負責」的組織，這會讓你不太自在；但如果你一直想要那種「你的程式碼 ship 給數百萬使用者、而且你能在同一週追到營收影響」的擁有感——就是這個。

---

## 你實際上會做什麼

**閉合意圖捕捉與營收之間的迴圈。** 這就是這份工作。以下所有事情都服務於這個使命。

- 以 **OpenAPI-first** 的方式設計並打造後端服務（Go / Python）——我們的 API 正朝 MCP 相容的 agent 介面演進，消費我們產品的不只是人，還有機器
- 打造捕捉使用者意圖的前端體驗（Vue.js / Nuxt.js）：AI 驅動的 Q&A widget、對話式流程、以及嵌入各媒體網站的 rich media 互動
- 把 LLM API 與 AI 模型整合進 production 功能——intent classification、sponsored question 媒合、conversational commerce——在真實規模上，而不是當實驗做
- 快速打造 AI 體驗的原型，並在**幾天內、而不是幾個月內，決定砍掉或 ship**。我們曾用 46 個串接的 API call、在 45 分鐘內產出一整套 AI 動畫產線。這就是我們期待的速度。
- 部署、監控並維運你打造的東西——Kubernetes（EKS）、Prometheus、Grafana、Sentry。你是第一線 responder，因為你就是最懂這個系統的人
- 把雲端成本當成產品限制來看待——我們橫跨 GCP、AWS 與 multi-cloud CDN 架構，FinOps 紀律在這裡是工程卓越的一部分
- 把 AI 工具當成你的預設工作流。Claude Code、Cursor（公司提供）與內部程式碼生成工具不是選配——這就是我們期待你工作的方式。如果你還在手刻 boilerplate，那就是太慢了。

---

## 我們在找的人

**不可妥協的條件：**

- 你端到端 ship 過 production 的 SaaS 產品——前端、後端、部署、監控。而且不只一次。是在「那不是我的工作」不成立的環境裡。
- 你在後端能自在使用 **Go 或 Python**、前端能自在使用 **Vue.js**。你今天不需要三者都是專家，但你要能在數週內、而不是數月內進入戰力。
- 你把 LLM API 或 AI 模型整合進真實使用者會碰到的 production 功能。
- 你用 **API contract 與系統介面**來思考，而不只是程式碼。你為那位還沒被招進來的下一個團隊成員做設計。
- 你的預設是 ship。當 brief 一團亂、需求只成形一半、沒人畫 wireframe——你做決定、做一版、放到使用者面前、然後迭代。「等到需求清楚為止」不在你的字典裡。

**會讓你脫穎而出的加分：**

- 有 **ad tech、martech 或出版變現**經驗——你懂為什麼意圖資料比曝光資料更值錢，也知道 CPM、CPC、ROAS 在實務上代表什麼
- 熟悉 **agent 框架與協定**（MCP、A2A、LangGraph、n8n），並對 AI-native 軟體架構的走向有自己的看法
- 你待過那種「你打造的產品，直接決定公司能不能募到下一輪、能不能簽下下一個客戶」的公司
- 中文溝通能力 — 我們團隊日常混用中英文，如果你能順暢地用中文討論技術方案、參與產品討論，會是很大的加分

---

## 技術棧

| 層 | 我們用什麼 |
|-------|-------------|
| Frontend | Vue.js / Nuxt.js / Vuex |
| Backend | Golang / Python / PostgreSQL / Redis |
| Infrastructure | EKS（Kubernetes）/ GCP / AWS / multi-cloud CDN 架構 |
| Observability | Prometheus / Grafana / Sentry / Loki |
| AI tooling | Claude Code / Cursor / 內部程式碼生成工具 |
| Data | Databricks / S3 clickstream pipeline / vector search |

我們的架構橫跨內容傳遞優化、即時行為資料捕捉，以及跨 multi-cloud 的 AI 模型編排。如果讓你興奮的是真正的系統複雜度——而不是玩具問題——這裡多的是。

---

## 為什麼是現在

我們正處在「引擎已被驗證」與「營收模式已被驗證」之間的轉折點。CDN 業務已經獲利；Intent Refinery 有真實使用者、真實資料，以及橫跨四個變現層的可運作原型。缺的是「被捕捉的意圖能轉化為品牌營收」的證明——而這個證明，決定了我們能不能募下一輪、如何進入美國市場、以及這家公司會變成什麼。

你前 90 天打造的功能，會出現在投資人簡報裡；你的程式碼所產生的資料，會出現在 pitch 裡。這不是修辭。

---

**想看看我們實際上怎麼打造這些？** → [我們怎麼做事：Becoming Product Builders with Business Thinking](../../how-we-ship.md)

---

## 如何應徵

寄給我們任何能展現你思考方式的東西——side project、技術文章、你引以為傲的 PR，或只是一段訊息解釋為什麼這個職位引起你的注意。我們在意的是你做過什麼，不是你待過哪裡。

📧 **[career@mlytics.com](mailto:career@mlytics.com)**
