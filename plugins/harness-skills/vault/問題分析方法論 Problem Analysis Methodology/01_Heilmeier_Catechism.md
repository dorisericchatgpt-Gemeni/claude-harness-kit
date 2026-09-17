---
title: Heilmeier Catechism — DARPA 8 問
type: methodology-note
category: research-question-formation
created: 2026-05-07
tags: [methodology, research-proposal, DARPA, grant-writing]
---

# Heilmeier Catechism

## 一句話定義

> A set of 8 questions developed by DARPA director George H. Heilmeier (1975–1977) that any research proposal must answer before being funded.

研究提案的「八項必答題」— 用最少的問題逼出一個研究計畫的核心價值、創新點、可行性、影響力。

## 起源

George Heilmeier 是液晶顯示器（LCD）的發明者之一，1975–1977 擔任 DARPA 主任。他發現大量研究提案文字漂亮但講不清楚「到底要做什麼、為什麼會成功」，於是制定這 8 題作為內部審查標準。後來被 NIH ARPA-H、NSF、各大研究機構廣泛採用。

## 核心問題清單（verbatim）

> 以下為原文，可直接拿來問自己 / 問學生 / 寫提案時對照：

1. **What are you trying to do?** Articulate your objectives using **absolutely no jargon**.
2. **How is it done today, and what are the limits of current practice?**
3. **What is new in your approach and why do you think it will be successful?**
4. **Who cares?** If you are successful, what difference will it make?
5. **What are the risks?**
6. **How much will it cost?**
7. **How long will it take?**
8. **What are the mid-term and final "exams" to check for success?**

### 中文解讀

| #   | 問題           | 真正在問什麼                             |
| --- | ------------ | ---------------------------------- |
| 1   | 用人話講你想做什麼    | 你**真的懂**自己在做什麼嗎？能不能對外行人講清楚？        |
| 2   | 現在怎麼做，極限在哪？  | 你有沒有真的讀過 SOTA？                     |
| 3   | 新點在哪，為什麼會成功？ | 你的 insight 是什麼？不是「沒人做過」而是「為什麼現在能做」 |
| 4   | 誰在乎？         | 成功了**誰會用 / 誰會引用 / 誰會付錢**？具體到一個人    |
| 5   | 風險？          | 最可能失敗的點，**你自己最怕的那一個**              |
| 6   | 多少錢？         | 設備 / 試劑 / 人力 / 算力，都算進去             |
| 7   | 多久？          | 含現實阻力（IRB、訂購、debug）                |
| 8   | 期中 / 期末怎麼驗收？ | 25%、50%、100% 各看什麼指標？               |

## ARPA-H 2022 擴充版（兩個新增題）

ARPA-H（NIH 健康版 ARPA）2022 加了兩題：

9. **How will cost, accessibility, and user experience be addressed** to ensure equitable access for all people?
10. **How might this program be misperceived or misused**, and how can we prevent that?

第 10 題是 dual-use 倫理檢查 — 對 BCI / 神經介面 / 基因編輯類研究特別重要。

## 何時用

- 寫研究計畫書（Aim section 之前先答完 8 題）
- 第一次跟教授講你的 idea
- 提交 grant proposal 前自我審查
- 一個專案動手前 30 分鐘的 sanity check

## 何時不用

- 你還在「探索式好奇」階段（this is curiosity-driven, not project-driven）
- 純理論工作沒有「成功怎麼定義」的明確指標時，Q4 / Q8 會卡住
- 對話初期 — 直接丟 8 題會壓垮對方，應該配合 [[07_Socratic_Method]] 拆成漸進式提問

## 常見誤用 / 失敗 pattern

| 表面回答 | 真實意思 | 該怎麼追問 |
|---|---|---|
| Q1 用一堆術語 | 自己沒想清楚 | "用高中生聽得懂的話再說一次" |
| Q2 「目前沒人做過」 | 不等於 novelty | "沒人做是因為沒人想到、做不到、還是試過沒發表？" |
| Q3 「我們有新方法」 | 沒講為什麼會成功 | "為什麼**現在**能做，5 年前不能？" |
| Q4 「對科學社群有貢獻」 | 模糊到無意義 | "點名一個人，他讀完你的 paper 之後會做什麼**不一樣**的事？" |
| Q5 「風險很低」 | 自欺 | 切換到 [[06_Pre_mortem]]：假設失敗了，列 5 個原因 |

## 與其他方法的關係

- **配合 [[02_FINER_PICO]]**：Heilmeier 偏「能不能說服 funder」，FINER 偏「研究問題本身結構」，兩者互補
- **配合 [[06_Pre_mortem]]**：Q5 風險題用 pre-mortem 來深挖
- **配合 [[15_Observable_Method_Fit]]**：Q3 「新方法」要展開到 observable / method fit 才完整
- **被 advisor-dialogue 使用**：作為 problem framing 的主骨架

## 給 learning-notes skill 的應用提示

當使用者問的是 **「我想研究 / 開發 X」** 類型題目時：

1. 在 `00_教學大綱總覽.md` 之前，先在 conversation 中走一輪 Heilmeier Q1–Q4
2. 在筆記的「目的 / 動機」section 必須能回答 Q1 + Q4
3. 在「現有技術回顧」section 必須能回答 Q2
4. 在「本研究 / 本筆記的新意」section 必須能回答 Q3
5. 如果 Q3 答不出來，這個主題可能不值得整理成深度筆記，建議改成簡短 reference

## 參考來源

- [The Heilmeier Catechism — DARPA 官方](https://www.darpa.mil/about/heilmeier-catechism)
- [The hidden questions behind the Heilmeier Questions — ARPA-H](https://arpa-h.gov/sites/default/files/2023-10/Qs_behind_the_HQs.pdf)
- [Creating Impactful One-Pagers Using the Heilmeier Catechism — Stanford](https://techtransferfordefense.stanford.edu/creating-impactful-one-pagers-using-heilmeier-catechism)
- [The Heilmeier Catechism — MIT MechE Comm Lab](https://mitcommlab.mit.edu/meche/2025/03/08/the-heilmeier-catechism/)
