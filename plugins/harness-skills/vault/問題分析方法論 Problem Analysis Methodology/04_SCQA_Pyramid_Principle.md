---
title: SCQA + Pyramid Principle — Minto 結構化溝通
type: methodology-note
category: problem-decomposition
created: 2026-05-07
tags: [methodology, communication, McKinsey, Minto, structured-writing]
---

# SCQA + Pyramid Principle

## 一句話定義

> **SCQA** (Situation, Complication, Question, Answer): A 4-step framework to define the **real** core problem before answering it.
> **Pyramid Principle**: A top-down communication structure where the answer (top) is supported by grouped, MECE arguments (middle) backed by evidence (bottom).

中文：**SCQA 用來找到問題、Pyramid 用來組織答案**。兩者是 Barbara Minto（McKinsey）方法論的雙核心。

## 起源

兩者都由 Barbara Minto 在 McKinsey 1960–70 年代開發，集大成於 *The Pyramid Principle: Logic in Writing and Thinking* (1987)。是顧問業、投行、product management 的標配寫作框架。

## SCQA — 找出真正的問題

### 核心問題清單

| 階段 | 原文 | 中文追問 | 例子 |
|---|---|---|---|
| **S**ituation | 讀者已經知道、不爭議的背景 | 你的 audience **沒爭議**接受的事實是什麼？ | 「Lab 目前用 wide-field imaging 看小腦活動」 |
| **C**omplication | 改變了 situation 的新事件 / 新發現 | 然後**發生了什麼**讓現狀不夠用？ | 「但 wide-field 解析度不足以區分單細胞 spike timing」 |
| **Q**uestion | 從 complication 自然浮現的問題 | 所以**真正要問的問題**是什麼？ | 「能不能用兩光子 16 Hz 達到單細胞解析度同時保留 timing 資訊？」 |
| **A**nswer | 你的論點 / 論文 / 建議 | 你的**一句話結論** | 「Yes — 用 GCaMP6f + Lissajous scanning」 |

關鍵：**Q 是被 S+C 邏輯「逼」出來的，不是你想問的**。如果讀者讀完 S 跟 C 後產生的問題不是你的 Q，代表你的 framing 沒對齊讀者。

### SCQA 變體

| 變體 | 強調 | 何時用 |
|---|---|---|
| **Standard** | S → C → Q → A | 中性論述 |
| **Direct** | A → S → C → Q | 結論先行（Pyramid 推薦） |
| **Concern** | S → Q → A → C | 強調憂患（提醒風險） |
| **Confidence** | A → C → Q → S | 強調解方信心 |

## Pyramid Principle — 組織答案

### 結構

```
                    [Governing Thought / Answer]
                              ↑
              ┌───────────────┼───────────────┐
        [Key Point 1]   [Key Point 2]   [Key Point 3]
              ↑               ↑               ↑
         [Evidence]      [Evidence]      [Evidence]
```

三條規則：

1. **Vertically — Q&A relationship**：上層的每一句話，下層必須能回答「為什麼？」或「怎麼做？」
2. **Horizontally — MECE & logical order**：同一層的 points 必須互斥窮盡（[[03_MECE_Issue_Tree]]），且有邏輯順序（時間 / 結構 / 重要性 / 演繹）
3. **Top-down summary**：每層都用一句 governing thought 概括下層，讓 audience 隨時可以「停在這層」也懂大意

### 核心問題清單（用來檢查自己的 pyramid）

寫完任何報告 / 論文 / proposal 後問自己：

1. 我的 governing thought（最上層那一句）是什麼？能不能用一句話講？
2. 支撐它的 key points 有幾個？是不是 3 個左右？
3. 這幾個 key points **彼此互斥嗎**？有沒有重疊？
4. 這幾個 key points **加起來窮盡嗎**？有沒有漏？
5. 它們之間是什麼**邏輯順序**？時間？結構？重要性？演繹？
6. 每個 key point 下面的 evidence，能不能直接回答「為什麼這個 key point 成立」？

## 整合應用：SCQA → Pyramid

完整的論述 = SCQA 開頭 + Pyramid 主體：

```
[SCQA] 引言一段
  S: 大家都知道...
  C: 但是發生了 X...
  Q: 所以我們該問...
  A: 我認為答案是 Y    ← 這個 A 就是 Pyramid 的 governing thought

[Pyramid] 主體
  Y 成立有 3 個理由：
    1. 理由一 + evidence
    2. 理由二 + evidence
    3. 理由三 + evidence

[結論] 因此 Y，下一步...
```

## 何時用

- 寫 paper abstract（SCQA 完美對應 abstract 結構：背景→問題→方法→結論）
- 給老闆 / 教授 30 秒簡報
- Grant proposal Specific Aims
- Technical write-up / blog post / 任何要說服人的文件

## 何時不用

- 探索性筆記（你還在發散，不是收斂）
- 對話中的腦力激盪（pyramid 太正式）
- 需要保持懸念的敘事（pyramid 結論先行，破壞 narrative）

## 常見誤用 / 失敗 pattern

| 錯誤 | 修正 |
|---|---|
| Q 是你想問的，不是 S+C 邏輯逼出來的 | 重寫 S 跟 C，讓讀者讀完自然產生你的 Q |
| Governing thought 太抽象（「我們發現有趣的結果」） | 改成 specific 結論（「16 Hz imaging 的 SNR 比 1 Hz 高 2.3 倍」） |
| Key points 不 MECE（重疊） | 套 [[03_MECE_Issue_Tree]] 重新切 |
| Bottom-up 寫法（先寫細節再結論） | Pyramid 是 top-down，從結論寫起 |
| 每個 key point 下面塞太多 evidence | 控制在 3 個 evidence，多的丟附錄 |

## 與其他方法的關係

- **配合 [[03_MECE_Issue_Tree]]**：Pyramid 的 horizontal 那層必須 MECE
- **配合 [[01_Heilmeier_Catechism]]**：Heilmeier Q1（用人話講你想做什麼）= Pyramid 的 governing thought
- **配合 [[08_Toulmin_Argumentation]]**：每一個 key point 都要能拆成 Toulmin 的 claim / grounds / warrant
- **被 advisor-dialogue 使用**：對話最後要使用者用 SCQA 收尾整理結論

## 給 learning-notes skill 的應用提示

當產出 **任何**學習筆記時：

1. 筆記開頭的「一句話定義 / Abstract」section 必須是 SCQA 結構（即使只有一段，要有 S, C, Q, A 四個成分）
2. 章節編排必須符合 Pyramid：先講結論（What），再講為什麼（Why），最後講細節（How）
3. 每個章節的開頭第一句必須是 governing thought（一句話總結這章在講什麼）
4. 章節之間的順序必須有邏輯（時間 / 結構 / 重要性），不能任意排列
5. 在 `00_教學大綱總覽.md` 的「章節順序」必須能用一句話解釋為什麼是這個順序

## 應用案例

- 韋伯式歷史制度分析法：用 SCQA 界定制度結果，再把歷史材料統一到可比較的因果問題。

## 參考來源

- [How SCQA and the Pyramid Principle Fit Into The Strategy Consulting Process — StrategyU](https://strategyu.co/how-scqa-and-the-pyramid-principle-fit-into-the-strategy-consulting-process/)
- [The Pyramid Principle — FunBlocks AI](https://www.funblocks.net/thinking-matters/classic-mental-models/the-pyramid-principle)
- [ModelThinkers — Minto Pyramid & SCQA](https://modelthinkers.com/mental-model/minto-pyramid-scqa)
- [Pyramid Principle & SCQA: A Consultant's Guide — Deckary](https://deckary.com/blog/pyramid-principle-consulting)
- Minto B., *The Pyramid Principle: Logic in Writing and Thinking* (1987)
