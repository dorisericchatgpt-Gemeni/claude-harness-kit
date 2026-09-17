---
title: Working Backwards (Amazon PR/FAQ) — 從終點反推
type: methodology-note
category: customer-driven-design
created: 2026-05-07
tags: [methodology, product-management, Amazon, Bezos, customer-centric]
---

# Working Backwards (Amazon PR/FAQ)

## 一句話定義

> Amazon's product development methodology in which teams **start by writing the customer-facing press release and FAQ** *before* any engineering begins — forcing clarity about the user benefit and iteratively refining the concept until it survives stakeholder scrutiny.

中文：在寫任何一行 code 或做任何實驗之前，先**假裝產品已經完成**，寫一份對外發布的新聞稿（PR）+ 常見問答（FAQ），用這份文件強迫自己想清楚「使用者到底為什麼要用？」

## 起源

Jeff Bezos 約 2004 年於 Amazon 推行。最早用於 AWS、Kindle、Prime Video 等大產品的內部審查。Colin Bryar 與 Bill Carr（前 Amazon 高管）2021 年寫成 *Working Backwards: Insights, Stories, and Secrets from Inside Amazon*，將這個 process 系統化公開。

## 核心結構：PR/FAQ 文件

### 1. Press Release（< 1 頁）

假裝產品已上市，**寫給外部讀者**的新聞稿，必含：

| 元素 | 內容 |
|---|---|
| Heading | 產品名稱 + 一句話 tag line |
| Sub-heading | 對誰、為了什麼好處 |
| Summary | 4 句話：什麼、誰用、為什麼好、怎麼開始用 |
| Problem | 顧客**現在**面對的問題（具體） |
| Solution | 你的產品**怎麼**解決 |
| Quote from your company | 為什麼這個產品重要（願景） |
| How to get started | 第一步是什麼 |
| Customer quote | **最重要的部分** — 一個假想顧客講為什麼喜歡（這逼出真正的價值） |
| Closing call to action | 怎麼開始用 |

### 2. FAQ（≤ 5 頁）

#### External FAQ — 顧客會問的

模擬顧客 / 媒體 / 評論員會問的問題：
- 「這跟競爭對手有什麼不同？」
- 「多少錢？」
- 「我為什麼要從 X 切換到這個？」
- 「相容性？」

#### Internal FAQ — 公司高層會問的

更難、更技術的問題：
- 「為什麼是**現在**做？」
- 「需要哪些技術突破？」
- 「Build vs buy？」
- 「3 年回本嗎？unit economics？」
- 「如果競爭對手 1 年內 copy 怎麼辦？」
- 「最大的風險是什麼？」
- 「需要哪些 dependency / 跨部門合作？」
- 「Adverse selection / regulatory / legal 風險？」

## 核心問題清單

寫 PR/FAQ 時逐一回答：

### 對顧客（External）
1. 我的目標顧客是**具體誰**？(不能寫「使用者」，要寫「30 歲、住北市、每週騎車通勤的工程師」)
2. 他們**現在**怎麼解決這個問題？
3. 我的方案讓他們**省什麼 / 賺什麼 / 爽什麼**？
4. 他們**第一次**用我的產品時會看到什麼？
5. 他們會跟朋友怎麼形容這個產品？(一句話)

### 對自己（Internal）
6. 為什麼是**現在**？什麼變了讓這件事可能？
7. 我們有什麼**不公平的優勢**做這件事？
8. 最大的**技術風險**？最大的**市場風險**？
9. 6 個月後 demo 什麼算 milestone？
10. 失敗時我們會學到什麼？

## Bezos 的關鍵原則

1. **顧客先、技術後**（不是「我們有什麼技術 → 賣給誰」，是「顧客需要什麼 → 我們怎麼做」）
2. **書面、不投影片**（強迫完整論述，不能用 bullet 跳過弱點）
3. **6 頁規則**（PR 1 頁 + FAQ ≤ 5 頁，逼濃縮）
4. **iteration**：PR/FAQ 通常重寫 5–10 版才核准
5. **PR/FAQ 過了才有預算 / 工程資源**

## 例子（你的領域：BCI 系統）

模擬一份 Working Backwards 文件給「閉迴路小腦 BCI 系統」：

**PR Heading**：
> 「Cerebellar BCI v1.0：用 16 Hz 兩光子鈣訊號控制游標，正確率達 92%」

**Sub-heading**：
> 「給 ALS 與 spinocerebellar ataxia 患者的非侵入式運動意圖解碼系統」

**Customer quote**：
> 「我以為再也不能跟孫子打字了。現在我用想的就能把字打出來，雖然慢，但是是**我自己**做到的。」 — 模擬病人 A

**Internal FAQ Q：「為什麼是現在做？」**
> GCaMP6f 的 SNR 在 2014 後達到 single-spike resolution；Lissajous scanning 2022 後可以做到 1×1 mm @ 30 Hz；機器學習解碼準確率 2024 後在 cerebellar data 上突破 90%。三個 enabler 同時 ready。

→ 寫完才發現：模擬病人 quote 寫不出具體 number → 表示產品定位還不夠 sharp，逼自己再 iterate。

## 何時用

- 啟動新產品 / 新系統 / 新 tool 之前
- 寫 grant proposal 的 Significance section
- 規劃論文要 sell 什麼 narrative
- 開源專案的 README（你的 README 就是 PR）
- 求職時的 self-pitch

## 何時不用

- 純基礎研究（沒有「使用者」，但仍可改成「未來引用者」視角）
- 已經 deep dive 進實作階段時
- 探索式 hackathon

## 常見誤用 / 失敗 pattern

| 錯誤 | 修正 |
|---|---|
| Customer quote 寫不出來 | → 你還不知道你的價值主張 |
| PR 太多技術術語 | → 回去寫人話版 |
| Internal FAQ 跳過難題 | → 越難的問題越要寫 |
| 沒寫 「為什麼現在」 | → 必補，否則該專案沒有 timing 論證 |
| 寫成「為什麼這個技術很酷」 | → 強迫從顧客 / 使用者角度重寫 |
| 投影片化（變成 bullet） | → 強制改回完整段落 |

## Working Backwards 在學術研究的變體

學術版 PR/FAQ：

| Amazon | 學術 |
|---|---|
| Press Release | 假想的論文 abstract（已發表） |
| Customer | 未來 5 年的引用者 |
| Customer quote | 引用者怎麼引用你（「Wang et al. (2027) demonstrated that...」） |
| External FAQ | 論文 reviewer 會問的問題 |
| Internal FAQ | 你 lab 老闆 / committee 會問的問題 |

## 與其他方法的關係

- **配合 [[01_Heilmeier_Catechism]]**：Heilmeier 是 funder 視角，Working Backwards 是 customer 視角，互補
- **配合 [[06_Pre_mortem]]**：PR/FAQ 寫的是「成功的樣子」，pre-mortem 寫「失敗的樣子」，雙向夾擊
- **配合 [[02_FINER_PICO]]**：PICO 的 O (outcome) ≈ PR 的 customer benefit
- **被 learning-notes skill 使用**：當使用者要做的是「build 一個系統 / tool」時主用

## 給 learning-notes skill 的應用提示

當使用者問的是 **「我想 build / 設計 / 開發 X」** 類型題目時：

1. 在筆記開頭新增 **「假想 PR (一年後的樣子)」** section（不超過半頁）
2. 必須有一個假想 customer quote — 寫不出來 → flag 警告價值主張不清楚
3. 在「Why now」section 必須回答 internal FAQ 「為什麼是現在做」
4. 在「風險 / 限制」section 必須包含 Internal FAQ 的難題
5. 學術版本：寫一個假想的「未來引用」（誰會 cite、怎麼 cite）

## 參考來源

- [The Amazon Working Backwards PR/FAQ Process](https://workingbackwards.com/concepts/working-backwards-pr-faq-process/)
- [Working Backwards PR/FAQ Instructions & Template](https://workingbackwards.com/resources/working-backwards-pr-faq/)
- [An insider look at Amazon's culture and processes](https://www.aboutamazon.com/news/workplace/an-insider-look-at-amazons-culture-and-processes)
- [Amazon Working Backwards Template — Hustle Badger](https://www.hustlebadger.com/what-do-product-teams-do/amazon-working-backwards-process/)
- [AWS Prescriptive Guidance: Start with why](https://docs.aws.amazon.com/prescriptive-guidance/latest/strategy-product-development/start-with-why.html)
- Bryar C. & Carr B., *Working Backwards: Insights, Stories, and Secrets from Inside Amazon* (2021)
