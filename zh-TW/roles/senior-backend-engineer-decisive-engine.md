<div style="display:flex;justify-content:space-between;align-items:baseline;margin-bottom:20px">
<a href="/zh-TW/">← 返回所有職缺</a>
<a href="/roles/senior-backend-engineer-decisive-engine.html">English</a>
</div>

# Senior Backend Engineer — Decisive Engine

## 30 秒認識 Mlytics

Mlytics 是一套 AI Answer Engine。我們幫媒體與出版業者把讀者意圖轉化為商業成果——用高品質的 CPL 收入，取代持續下滑的 CPM 收入。我們的 Intent Refinery 已在 15+ 家台灣頭部媒體上線，服務 4M+ 週活躍使用者。

我們從 multi-CDN 起家。那套基礎設施——<50ms 路由、multi-vendor failover——現在是整個產品的技術底層。

[更認識 Mlytics →](../README.md)

---

## 這個角色

Decisive Engine 是 Mlytics 最有價值的系統之一，也是 multi-CDN 產品背後的後端決策層：即時 routing、scoring、contextual bandit、attribution，以及讓這些決策持續流動的 Kafka / Redis / ClickHouse data path。

這不是一個接手乾淨 service、只需要在邊緣增加 endpoint 的職位。你會成為一套承載 PB 級流量、已被市場驗證的複雜系統之主要技術 owner——理解它為什麼被做成現在的樣子，保留仍然有效的部分，挑戰已經不再合理的決策，並讓它變得更快、更安全、更有能力。

下一章不是 maintenance。我們要讓這個引擎能被 agent 生態取用：**今天 OpenAPI-first，下一步是 MCP-compatible 介面與 A2A 的可能性。** 你的工作，是做深現有的後端，也為它在 agent 時代需要的新介面開路。

---

## 你實際上會做什麼

**接下核心決策引擎，然後把它往前推。**

- 擁有並演進橫跨 **routing、scoring、contextual bandit 與 attribution** 的即時決策管線；隨流量成長，持續維持決策的穩定、正確、可觀測與低延遲。
- 使用 **Go / Python、PostgreSQL / Redis、Kafka、ClickHouse 與 EKS** 設計並優化高吞吐服務及資料流。你處理的是 concurrency、state、attribution latency、candidate cardinality 與水平擴展，而不只是 CRUD API。
- 不等待全面重寫，也能改善大型既有系統。補上測試、observability、migration path 與架構接縫，讓它在持續服務 production 的同時仍能安全演進。
- 把產品往 agentic 介面推進：設計 **OpenAPI-first** contract，驗證 MCP-compatible 存取與 A2A 整合，並用最小實作判斷新的接入面能不能創造真實價值。
- 把 **Claude Code、Cursor 與其他 AI 工具當成預設開發工作流**。AI 用來放大產出而不是取代工程判斷；有效的方法也應該沉澱成整個團隊能重複使用的知識。
- 在沒有獨立 DevOps function 的團隊裡端到端擁有功能：scope、設計、實作、CI/CD、部署、observability、on-call、incident response，以及 production feedback 之後的收尾。
- 把效能與成本當成產品的一部分。讓 latency、compute、storage 與 reliability 之間的取捨可見，再用證據改善單位流量成本。

---

## End-to-end 也包含 production

設計 decision path 的人，也應該知道它在真實流量下如何運作。你會分擔自己所擁有服務的 on-call；當決策管線 degraded 時回應、恢復服務，並把事故轉化為長久有效的改善——程式、監控、自動化或 runbook。

這不是一個以 operations 為主的職位，成功也不以救了多少次火衡量。Production ownership 是讓你成為更強 backend engineer 的 feedback loop：它會揭露架構圖看不到的 failure mode、performance cliff、hidden coupling 與成本假設。

---

## 我們在找的人

**不可妥協的條件：**

- 5 年以上資深後端工程經驗，具備 **distributed systems、高併發與即時資料處理**的實戰經驗。
- 深度熟悉 **Go 或 Python**，並具備紮實的 concurrency、data structure、algorithm 與 system design 基礎。
- 有多項 **PostgreSQL、Redis、Kafka、ClickHouse、Kubernetes（EKS）、GCP 與 AWS** 的 production 經驗；能橫跨整條路徑思考 throughput、latency、state、failure 與 cost。
- 曾接手並演進大型或複雜既有後端。你知道如何建立 context、降低風險、改善架構，而不會把 greenfield 當成唯一有成就感的工作。
- 有 AI / LLM 整合，或 **RAG、MCP、agent interface** 等技術實作經驗，且 AI 工具已經是你日常開發軟體的方式之一。
- 能把模糊的產品問題切成可行 scope，在低度監督下端到端 ship。

**會讓你脫穎而出的加分：**

- 有 routing、scoring、online learning / contextual bandit、attribution、multi-CDN，或其他同時要求 latency 與 correctness 的即時決策引擎經驗。
- 曾把後端架構連結到商業結果：客戶留存、gross margin、基礎設施單位成本，或新的產品接入面。
- 有定義 OpenAPI contract，並將既有能力轉化為其他 service 或 agent 能可靠取用之介面的經驗。
- 會透過 code review、文件或技術分享主動擴散 AI 輔助開發實踐，讓身邊的工程師一起變快。
- 能以中文／華語與團隊溝通會是明顯加分。

**如果以下描述像你，這個角色可能不適合：**

- 你只想做 greenfield，比起理解與改善成熟系統，更想直接重寫。
- 你把 AI coding tools 視為威脅或選配實驗，而不是現代工程工作流的一部分。
- 你認為 code merge 就是工作結束，deployment、performance、cost 與 production behavior 應該由別人負責。
- 你只優化技術上漂亮的產出，卻不問它改變了產品、使用者或商業上的什麼。

---

## 技術棧

| 層 | 我們用什麼 |
|-------|-------------|
| Core services | Go / Python |
| Decision systems | Routing / scoring / contextual bandits / attribution |
| Data path | Kafka / Redis / ClickHouse / PostgreSQL |
| Infrastructure | EKS（Kubernetes）/ GCP / AWS / multi-cloud CDN architecture |
| Observability | Prometheus / Grafana / Sentry / Loki |
| Agent interfaces | OpenAPI / MCP-compatible services / A2A exploration |
| AI tooling | Claude Code / Cursor / 內部程式碼生成工具 |

工具是真的，但這份工作比 stack 更大。我們需要的是能跨越 service、data 與 infrastructure，追完一次 routing decision，並且仍能說清楚這個決策為什麼對產品重要的人。

---

## 怎樣算是做得好

- 隨流量與決策複雜度成長，Decisive Engine 仍然可用、正確、低延遲。
- p99 latency 與單位流量成本改善，因為系統被更深入理解，也被有意識地優化。
- Feature 與 fix 從設計到 production 的速度加快，同時沒有增加事故、回歸缺陷或 MTTR。
- 一個具體的 OpenAPI / MCP milestone，讓決策引擎的部分能力可透過 agent-compatible 介面取用。
- 你能在低度監督下端到端擁有有意義的 service 或 module，包括它在 production 的表現。
- AI-native 開發實踐不只提高你的速度，也透過文件化、可重複使用的 pattern 提高團隊速度。

---

## 為什麼是現在

Mlytics 從 multi-CDN routing 起家。這套決策引擎不是在公司往前走時勉強維持的 legacy——它正是下一個產品建立其上的後端基礎。

這個角色的工程師會決定：這套基礎只是撐過成長，還是成為更深的產品能力——更快的決策、更好的 unit economics、更安全的迭代，以及 agent 時代的新介面。如果你想接下一個困難的系統、讓它明顯變得更好，並從中打開下一個產品接入面，就是這份工作。

---

**想看看我們實際上怎麼打造這些？** → [我們怎麼做事：Becoming Product Builders with Business Thinking](../../how-we-ship.md)

---

## 如何應徵

寄給我們任何能展現你怎麼思考後端系統的東西——一個你接手過的複雜服務、你解過的 latency 或 concurrency 問題、一場改變了你設計的 production incident，或一套你真正落地的 AI-native 工作流。我們在意你 ship 了什麼、量測了什麼，以及因為你的 ownership，什麼真的變得更好。

📧 **[career@mlytics.com](mailto:career@mlytics.com)**
