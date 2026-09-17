---
title: Bloom's Taxonomy — 認知層次六級
type: methodology-note
category: cognitive-depth
created: 2026-05-07
tags: [methodology, education, cognitive-science, Bloom, learning]
---

# Bloom's Taxonomy

## 一句話定義

> A 6-level hierarchy of cognitive learning objectives — Remember → Understand → Apply → Analyze → Evaluate → Create — used to ensure that questions, assessments, and learning activities target appropriate depths of thinking, not just rote recall.

中文：六級認知層次階梯，用來檢查問題 / 學習活動是停在「背誦」層還是真的進到「分析、評估、創造」層。

## 起源

- **原版 (1956)**：Benjamin Bloom 領導的教育學家委員會發表 *Taxonomy of Educational Objectives*。原版六級為：Knowledge, Comprehension, Application, Analysis, Synthesis, Evaluation。
- **修訂版 (2001)**：Anderson & Krathwohl 等人修訂，將名詞改為動詞、調整順序、把 Synthesis 改成 Create 並放最頂層。

修訂版（現行標準）：
**Remember → Understand → Apply → Analyze → Evaluate → Create**

## 六層核心問題清單

### Level 1 — Remember（記憶）

**動作**：recall, recognize, list, name, identify, define

**問題模板**：
- 「X 的定義是什麼？」
- 「列出 X 的三個特徵」
- 「誰提出 X？什麼時候？」

例子（你的領域）：「GCaMP6f 的 Kd 是多少？」

### Level 2 — Understand（理解）

**動作**：explain, summarize, paraphrase, classify, compare

**問題模板**：
- 「用你自己的話解釋 X」
- 「X 和 Y 的差別是什麼？」
- 「為什麼 X 會發生？」

例子：「為什麼 GCaMP 比 OGB-1 適合 chronic imaging？」

### Level 3 — Apply（應用）

**動作**：use, implement, execute, solve, demonstrate

**問題模板**：
- 「在 [新情境] 中怎麼用 X？」
- 「給定 [參數]，計算 X」
- 「用 X 解決 [具體問題]」

例子：「給定 16 Hz 取樣率與 GCaMP6f 動力學，估算可偵測的最高 spike rate」

### Level 4 — Analyze（分析）⭐ 開始進入 critical thinking

**動作**：differentiate, organize, attribute, deconstruct

**問題模板**：
- 「X 由哪些**部件**組成？它們怎麼互動？」
- 「X 的**隱藏假設**是什麼？」
- 「X 跟 Y 的差異**為什麼重要**？」
- 「這個現象的 root cause 是什麼？」

例子：「Lissajous scanning 跟 raster scanning 在 SNR、speed、coverage 上的 trade-off 是怎麼來的？」

### Level 5 — Evaluate（評估）⭐⭐ 高階 critical thinking

**動作**：critique, judge, justify, defend, rank

**問題模板**：
- 「X 跟 Y 哪個更好？**根據什麼判準**？」
- 「X 的論證**站得住**嗎？最弱的點？」
- 「如果你是 reviewer，會接受 X 嗎？」
- 「X 的**證據強度**有多強？」

例子：「兩光子 vs 三光子 imaging 在 cerebellar imaging 上哪個比較適合？根據什麼判準？」

### Level 6 — Create（創造）⭐⭐⭐ 最高層

**動作**：design, construct, plan, produce, invent

**問題模板**：
- 「**設計**一個 X 來解決 Y」
- 「**結合** A 跟 B 產生新的 C」
- 「如果 X 不存在，**發明**一個替代品」
- 「**提出**新的研究問題 / 新的假說」

例子：「設計一個 imaging protocol 同時量到 cerebellar Purkinje cell + DCN cell + behavior，列出 trade-offs 與 mitigation」

## 視覺化：金字塔

```
                 ┌──────────────┐
                 │   CREATE     │ ⭐⭐⭐ 設計、產生新東西
              ┌──┴──────────────┴──┐
              │     EVALUATE       │ ⭐⭐ 判斷、批判
           ┌──┴────────────────────┴──┐
           │       ANALYZE             │ ⭐ 拆解、找關係
        ┌──┴───────────────────────────┴──┐
        │           APPLY                  │ 用知識解新問題
     ┌──┴──────────────────────────────────┴──┐
     │            UNDERSTAND                    │ 解釋、轉述
  ┌──┴──────────────────────────────────────────┴──┐
  │              REMEMBER                            │ 背誦、辨識
  └──────────────────────────────────────────────────┘
```

## 「Higher-Order Thinking Skills (HOTS)」分界

學界共識：**Analyze + Evaluate + Create = 高階思考**。研究 / 學術工作的目標就是讓自己跟學生**儘快上到 Level 4 以上**。停在 1–3 層的工作就是「複習考」、不是真正的研究。

## 何時用

- 設計學習目標 / 課綱
- 寫考題 / 評量設計（確保涵蓋 4–6 層，不只 1–3）
- 自我學習檢查（「我對 X 的理解到哪一層？」）
- 帶學生 / 寫教材時確保不只停在記憶層
- 寫筆記時的章節深度檢查

## 何時不用

- 純技能訓練（如儀器操作 SOP，停在 Apply 就夠）
- 不需要區分認知層次的純資訊查詢

## 核心問題清單（自我檢查）

對任何學習材料 / 自己寫的筆記問：

1. 我這份筆記**最高停在哪一層**？
2. 有沒有 Analyze 層的問題？(拆解、找隱藏假設)
3. 有沒有 Evaluate 層的問題？(批判、判準)
4. 有沒有 Create 層的延伸題？(設計新研究)
5. 如果只到 Understand 層，這份筆記是「教科書複習」而非「研究筆記」

## 常見誤用 / 失敗 pattern

| 錯誤 | 修正 |
|---|---|
| 自以為在 Analyze 其實只是 Understand | 「拆解」要找出**隱藏連結**，不只是列部件 |
| Evaluate 只是「我覺得 X 比較好」 | 必須有**明確判準**，且解釋為什麼用這個判準 |
| Create 跟 brainstorm 混淆 | Create 要有結構、約束、可執行；brainstorm 是 divergent |
| 用低階問題評估高階學習 | 考試只考 Remember 卻期待學生 Create |
| 跳級（沒打基礎就上 Analyze） | 1–3 層要先穩固，否則 4–6 層是空中樓閣 |

## 與其他方法的關係

- **配合 [[07_Socratic_Method]]**：Socratic 提問必須打到 Level 4–6，不能停在 1–3
- **配合 [[01_Heilmeier_Catechism]]**：Heilmeier Q3「what's new」 = Create 層；Q5「risks」 = Evaluate 層
- **配合 [[08_Toulmin_Argumentation]]**：Toulmin 拆解 = Analyze；判斷 warrant 強度 = Evaluate
- **被 learning-notes skill 使用**：作為筆記深度的標尺
- **被 advisor-dialogue 使用**：advisor 提問必須打到 Level 4 以上

## 給 learning-notes skill 的應用提示

每份筆記產出後做 Bloom 檢查：

1. 在筆記末尾加一個 **「Bloom 層次自我檢查」** mini-section
2. 列出本筆記涵蓋的 Bloom 層次（打勾）
3. 如果只到 Level 3 → 警告：這只是 reference notes，不是研究筆記
4. 在「延伸思考 / 練習題」section 必須包含 Level 4–6 的問題各一題：
   - Analyze 題：拆解 X 的組件 / 假設
   - Evaluate 題：比較 X 與 Y、判定優劣
   - Create 題：基於 X 設計新東西 / 新研究

## 應用案例

- 韋伯式歷史制度分析法：以 L4 因果拆解、L5 反例評估和 L6 制度比較檢查是否超越背誦。

## 參考來源

- [Bloom's Revised Taxonomy — Colorado College](https://www.coloradocollege.edu/other/assessment/how-to-assess-learning/learning-outcomes/blooms-revised-taxonomy.html)
- [Bloom's Taxonomy — Simply Psychology](https://www.simplypsychology.org/blooms-taxonomy.html)
- [Bloom's taxonomy of cognitive learning objectives — PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC4511057/)
- [Higher Order Thinking: Bloom's Taxonomy — UNC Learning Center](https://learningcenter.unc.edu/tips-and-tools/higher-order-thinking/)
- [Bloom's Taxonomy — Wikipedia](https://en.wikipedia.org/wiki/Bloom's_taxonomy)
- Anderson L.W. & Krathwohl D.R., *A Taxonomy for Learning, Teaching, and Assessing* (2001)
- Bloom B.S., *Taxonomy of Educational Objectives* (1956)
