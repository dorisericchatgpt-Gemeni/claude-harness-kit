---
title: Popper Falsifiability — 可證偽性
type: methodology-note
category: research-question-formation
created: 2026-05-07
tags: [methodology, philosophy-of-science, Popper, falsifiability, hypothesis]
---

# Popper Falsifiability

## 一句話定義

> Karl Popper's demarcation criterion: a theory is **scientific** if and only if it makes predictions that **could in principle be shown to be false** by observation. Theories that explain everything (and forbid nothing) are not scientific.

中文：一個假說是科學的，**當且僅當它能被觀察 / 實驗推翻**。如果不管結果怎樣都能解釋，它就不是科學。

## 起源

Karl Popper (奧地利-英國哲學家) 在 *Logik der Forschung* (1934, 英譯 *The Logic of Scientific Discovery*, 1959) 提出。動機：他發現 Marxism、Freudian psychoanalysis、Adler 心理學「**任何證據都能解釋**」，反而是 Einstein 廣義相對論做出**具體可被推翻**的預測（光線在重力場彎曲），於是提出「falsifiability」作為**科學 vs 偽科學的分界線**。

## 核心思想

### 為什麼 verification 不夠？

> 「**1000 隻白天鵝**不能證明『所有天鵝是白的』」
> 「**1 隻黑天鵝**就能推翻『所有天鵝是白的』」

歸納法（驗證法）有結構性弱點：再多正例都不能保證結論。但**一個反例就足以推翻全稱命題**。所以科學的進展依賴「找反例 / 嘗試 falsify」，不是「累積支持」。

### Falsifiability 的兩個層次

| 層次 | 意義 |
|---|---|
| **In principle falsifiable** | 邏輯上**存在**某種可能的觀察結果會推翻它 |
| **In practice falsifiable** | 我們**現在**就能設計出實驗去推翻它 |

Popper 認為前者就足夠當「科學」的判準；後者是「好的科學」的判準。

## 核心問題清單

對任何假說 / 理論 / 結論問：

1. **什麼樣的觀察結果會讓你放棄這個假說？** （← 最重要）
2. 這個假說**禁止**什麼事情發生？(forbidding power = scientific power)
3. 你的假說有多 **risky**？(預測越具體、風險越高、科學價值越高)
4. 如果你的預測**沒成立**，你會 (a) 放棄假說 (b) 加 ad hoc 補丁 (c) 怪實驗？哪一個是誠實的反應？
5. 你能不能**設計一個實驗**，**任何結果**都不會推翻你的假說？如果可以 → 你的假說不是科學的

## 例子

### Popper 的經典對比

| 「科學」 | 「偽科學」 |
|---|---|
| 「光線在重力場會彎曲 1.75 弧秒」 | 「精神病是 unconscious 衝突造成的」 |
| 可被 1919 日食實驗推翻 | 任何行為都能事後解釋 |
| Risky prediction | 不可被反例推翻 |

### 你的領域應用

**有 falsifiability 的假說（好）**：
> 「Cerebellar Purkinje cell 的 spike rate 在 reaching task 期間會在 movement onset 前 100±50 ms 顯著升高。」

→ 如果量到的 firing rate 在 onset 後才升、或完全沒升，**這個假說就被推翻**。

**沒有 falsifiability 的假說（壞）**：
> 「小腦參與 motor learning。」

→ 不管量到什麼結果都能解釋。「沒看到？因為這個 task 沒涉及」「看到了？小腦果然參與」 → 不是科學陳述

## 何時用

- 寫研究 hypothesis 時自我檢查
- 讀論文時檢驗作者的 claim
- 設計實驗時確保**有可能失敗**（沒有失敗可能性的實驗沒科學價值）
- 寫 grant proposal 的 Aims（每個 Aim 必須能被推翻）

## 何時不用 / 限制

Popper 自己也承認的限制：

1. **Quine-Duhem thesis**：理論不能孤立測試 — 任何「失敗」都可以歸咎於 auxiliary assumptions（儀器、設定、protocol），不一定是核心理論錯
2. **Probabilistic theories**：機率性假說（如「吸菸增加肺癌風險 30%」）難以單一實驗 falsify
3. **Lakatos critique**：科學家實務上**不會**因為一個反例就放棄理論（會修補 protective belt），所以 strict falsification 太嚴格
4. **形式科學（數學、邏輯）不適用**

不過這些限制不否定 falsifiability 的核心價值 — 它仍是**最有用的單一判準**。

## 「Risky Prediction」概念

Popper 強調：**好的假說做 risky predictions**。

| 假說 A | 假說 B |
|---|---|
| 「藥物會改善病情」 | 「藥物在 60% 受試者使 HbA1c 下降 ≥ 0.8%，6 週內」 |
| 模糊、難 falsify | 具體、容易 falsify、若成立資訊量大 |

→ 假說越**敢預測具體數字**，越科學、越有價值。

## 常見誤用 / 失敗 pattern

| 錯誤 | 修正 |
|---|---|
| 假說寫成「X 影響 Y」（沒方向、沒大小） | 改成「X 增加 Y 至少 Z%，在條件 W 下」 |
| 結果不如預期就改假說 | 誠實面對：是 hypothesis 錯、還是 setup 有問題？分清楚 |
| 用 ad hoc 補丁救假說 | Popper 認為這就是 pseudo-science 的特徵 |
| 把 unfalsifiable 當優點（「我的理論能解釋一切」） | 紅旗！能解釋一切的理論等於不能預測任何事 |
| 把 statistical insignificance 當成 falsification | p > 0.05 是「沒有證據反對」不是「證據反對」(absence of evidence) |

## Pre-registration 與 Popper 的關係

近年「pre-registration」運動（在實驗前公開假說、分析計畫）就是 Popper 主義的實踐：

- 預先註冊**強迫**你寫 risky predictions
- 防止 HARKing (Hypothesizing After Results are Known)
- 防止事後改假說救 publication

→ 寫筆記 / 計畫實驗時，把假說寫到「pre-registration 等級」(具體 + 可推翻 + 預先承諾) = Popper 精神的實踐

## 與其他方法的關係

- **配合 [[02_FINER_PICO]]**：PICO 的 O 必須夠具體才能 falsify
- **配合 [[08_Toulmin_Argumentation]]**：Toulmin 的 Rebuttal section 對應 Popper 的 falsification conditions
- **配合 [[14_DOE_Confounding]]**：DOE 提供「公平 falsification」的設計原則
- **配合 [[09_Steelman_Red_Team]]**：Red Team 主動找 falsification 條件
- **被 advisor-dialogue 使用**：當使用者提出假說時，必問「什麼結果會推翻它」

## 給 learning-notes skill 的應用提示

當筆記涉及 **假說 / 預測 / 理論** 時：

1. 必須有一個 **「Falsification 條件」** section
2. 列出 specific 的觀察結果（含數字）會推翻假說
3. 如果列不出來 → 警告：這個假說不是 scientific，需要 reformulate
4. 在「實驗設計」section 必須說明這個實驗**有可能失敗**（不是設計成必成功的）
5. 「Risky prediction」原則：假說越具體越好，模糊假說退稿

## 應用案例

- [[24_Weber_Historical_Institutional_Analysis/02_韋伯式經濟史分析方法|韋伯式歷史制度分析]]：以西／東歐、英國／美國、中國／歐洲等對照排除市場、技術、人口的單因敘事。

## 參考來源

- [Falsifiability — Wikipedia](https://en.wikipedia.org/wiki/Falsifiability)
- [Falsifiability — Karl Popper's Basic Scientific Principle (Explorable)](https://explorable.com/falsifiability)
- [Criterion of falsifiability — Britannica](https://www.britannica.com/topic/criterion-of-falsifiability)
- [Popper's falsification and corroboration — arXiv](https://arxiv.org/pdf/2007.00238)
- [Popper — Sussex (Dienes)](http://www.lifesci.sussex.ac.uk/home/Zoltan_Dienes/inference/Popper.html)
- Popper K., *The Logic of Scientific Discovery* (1959, original German 1934)
- Popper K., *Conjectures and Refutations* (1963)
