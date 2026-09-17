---
title: FINER + PICO — 醫學研究問題篩選
type: methodology-note
category: research-question-formation
created: 2026-05-07
tags: [methodology, research-question, clinical-research, FINER, PICO]
---

# FINER + PICO

## 一句話定義

> **FINER**: A 5-criterion checklist (Feasible, Interesting, Novel, Ethical, Relevant) for evaluating whether a research question is worth pursuing.
> **PICO / PICOT**: A 4–5 element template (Population, Intervention, Comparison, Outcome, [Time]) for structuring a clinical research question.

兩者組合：**FINER 篩選問題值不值得做、PICO 把問題寫成可執行格式**。

## 起源

- **FINER**：Hulley, Cummings 等 *Designing Clinical Research* (1988) 教科書提出，後成為 NIH / 醫學院標準
- **PICO**：Sackett (1996) 提出 evidence-based medicine 框架，後擴充為 PICOT

## 核心問題清單（verbatim + 中文）

### FINER 五準則

| 準則              | 原文核心問題                                                                     | 中文追問                                            |
| --------------- | -------------------------------------------------------------------------- | ----------------------------------------------- |
| **F**easible    | Is the study **feasible** with available subjects, expertise, time, money? | 你**真的**有受試者 / 樣本 / 設備 / 時間 / 經費嗎？沒有，找誰要？拿不到怎麼辦？ |
| **I**nteresting | Will the answer **interest** the investigator, peers, community?           | 對誰有趣？你的指導教授？領域內 50 個專家？grant panel？讀者？          |
| **N**ovel       | Will the question provide **new** findings, or confirm/refute prior work?  | 真的新嗎？還是 reskin 已發表的東西？是 confirm 還是 refute？      |
| **E**thical     | Will an IRB / IACUC approve? Is informed consent feasible?                 | IRB / IACUC 過得了嗎？有 dual-use 風險嗎？data privacy？   |
| **R**elevant    | Will the answer **advance** scientific knowledge, policy, or practice?     | 答完之後**誰會做不一樣的事**？沒有人改變行為的話，relevant 等於零         |

### PICO / PICOT 結構

| 元素               | 中文     | 例子（臨床）       | 例子（你的領域：神經影像）                         |
| ---------------- | ------ | ------------ | ------------------------------------- |
| **P**opulation   | 對象     | 65 歲以上糖尿病患者  | 4–8 週齡 C57BL/6 公鼠                     |
| **I**ntervention | 介入     | 服用 metformin | 16 Hz 雙光子鈣訊號成像                        |
| **C**omparison   | 對照     | 安慰劑 / 標準療法   | 1 Hz 鈣訊號 / wide-field imaging         |
| **O**utcome      | 結果指標   | HbA1c 下降幅度   | SNR per neuron / motion artifact rate |
| **T**ime         | 時間（選用） | 12 週         | 30 分鐘連續錄影                             |

寫成一句話的 PICO 格式：

> 「In [P]，does [I] compared to [C] affect [O] over [T]?」

例子（小腦 BCI 研究）：
> 「In normal C57BL/6 mice with cerebellar GCaMP6f expression, does 16 Hz two-photon imaging compared to 1 Hz imaging affect motion-artifact-corrected SNR per Purkinje cell over 30-minute recording sessions?」

## 何時用

- **FINER**：題目選定**之前**，刪掉那些看起來吸引但根本做不出來 / 沒人在乎的題目
- **PICO**：題目選定**之後**，把模糊的「我想研究小腦」逼成一句結構化問題
- 寫 grant proposal 的 Specific Aims 第一段
- 給指導教授第一次提案前自我檢查

## 何時不用

- 純理論 / 數學研究（沒有 Population、沒有 Intervention）
- 探索性質的 imaging study（沒有預設 outcome）
- 工程系統 build（用 [[11_Working_Backwards]] 比較合適）

## 常見誤用 / 失敗 pattern

| 表面回答 | 真實意思 | 該怎麼追問 |
|---|---|---|
| F: 「應該可以做」 | 沒實際盤點資源 | 列出每一項：受試者 N=? 設備時數=? 經費=? 還缺什麼？ |
| I: 「我覺得很有趣」 | 自我中心 | 你的興趣不算數。**誰**會在乎？指導教授？grant panel？臨床醫師？ |
| N: 「PubMed 沒人做過」 | 缺席不等於 novelty | 沒人做可能是因為(a)沒人想到 (b)做不到 (c)做了沒發表 (d)做了被 reject。哪一個？ |
| E: 「應該不用 IRB」 | 沒查清楚 | 動物 / 人 / 公開資料各有不同規範。寫信問 IRB office。 |
| R: 「對基礎科學有意義」 | 模糊 | 答完之後 next paper 是什麼？next clinical trial 是什麼？ |
| PICO: O 寫成「看看會不會 work」 | outcome 沒定義 | 用什麼**單位**量？多大的差異算 effect？ |

## 與其他方法的關係

- **配合 [[01_Heilmeier_Catechism]]**：Heilmeier Q4 「who cares」≈ FINER R；Heilmeier Q5 「risks」≈ FINER F
- **配合 [[12_Popper_Falsifiability]]**：PICO 的 O 必須是可被 falsify 的（夠 specific 才能被推翻）
- **配合 [[15_Observable_Method_Fit]]**：PICO 的 O ≈ observable，I ≈ method
- **被 advisor-dialogue 使用**：作為 problem framing 的第二層篩選（在 Heilmeier 之後）

## 給 learning-notes skill 的應用提示

當使用者問的是 **「我想做一個實驗 / 臨床研究」** 類型題目時：

1. 在筆記開頭新增一個 **「Research Question (PICO 格式)」** section，把問題逼成一句話
2. 在「為什麼做這個研究」section 用 FINER 五點檢查
3. 如果 N 答不出來 → 這篇筆記應該定位為「文獻回顧 / 教科書複習」而非「研究計畫」
4. 如果 R 答不出來 → 警告使用者這個題目可能不該做
5. PICO 的 O 寫不出單位的話，連到 [[15_Observable_Method_Fit]] 強迫釐清

## 參考來源

- [FINER: a Research Framework — Elsevier](https://scientific-publishing.webshop.elsevier.com/research-process/finer-research-framework/)
- [Back to the basics: guidance for formulating good research questions — PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC11129835/)
- [FINER criteria – What does it mean? — Cosmoderma](https://cosmoderma.org/finer-criteria-what-does-it-mean/)
- [Formulating a researchable question — PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC3140151/)
- Hulley SB et al., *Designing Clinical Research* (4th ed., 2013)
- Sackett DL et al., *Evidence-based medicine: how to practice and teach EBM* (1996)
