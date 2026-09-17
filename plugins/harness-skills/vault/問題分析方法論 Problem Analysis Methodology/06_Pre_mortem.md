---
title: Pre-mortem — Klein 假設失敗回推法
type: methodology-note
category: failure-prediction
created: 2026-05-07
tags: [methodology, decision-making, risk-analysis, Gary-Klein, prospective-hindsight]
---

# Pre-mortem

## 一句話定義

> A risk-discovery technique developed by Gary Klein where, before a project starts, the team **stipulates that the project has already failed** and lists every plausible reason why — leveraging *prospective hindsight* to expose risks that conventional risk reviews miss.

中文：在專案啟動**之前**，假裝它**已經失敗了**，逆推為什麼會失敗。

## 起源

Gary Klein（決策心理學家、自然主義決策理論奠基者之一）2007 年於 *Harvard Business Review* 發表 *Performing a Project Premortem*。核心發現：研究顯示「prospective hindsight（事後諸葛的提前版）」可讓人想出失敗原因的能力提升 **30%**。

## 為什麼 work？關鍵心理學差異

| 普通風險評估 | Pre-mortem |
|---|---|
| 問：「**可能**會出什麼錯？」 | 問：「**已經**出了什麼錯？」 |
| 樂觀偏誤、避免唱衰 | 失敗已成事實，講真話沒社交成本 |
| Group think | 個別書寫 → 沒有團體壓力 |
| 「應該還好吧」 | 「我**早就**覺得 X 會出事」 |

## 核心問題清單（Klein 標準流程）

### 4 步驟操作（20–30 分鐘）

1. **設定前提（Set the premise）**
   告訴所有人：「**想像現在是 [X 個月後]，這個專案已經徹底失敗了**。不只是表現不佳 — 是**慘敗**。讓這個事實沉澱一下。」

2. **個別書寫（Independent writing, 2–3 min）**
   每個人**獨自**寫下所有他能想到的失敗原因。**必須先寫再分享**，避免從眾。

3. **輪流分享（Round-robin sharing）**
   每人輪流講**一條**理由（不要一次講完），寫到白板上。重複輪流直到沒人有新點。

4. **整合與行動**
   - 找出**重複出現**的 cause（高風險訊號）
   - 找出**沒人想到但有人提出**的（盲點）
   - 對每個 high-risk cause 列出**現在可以採取的 mitigation**

### 提問模板（直接套用）

> 「想像現在是 [12 個月後]。這個專案徹底失敗了。
>
> 1. 它是怎麼失敗的？(描述失敗的樣子)
> 2. 失敗的 5 個原因是什麼？(逐一列出)
> 3. 這 5 個原因裡，哪些是**我們早該預料到**的？
> 4. 哪些是**我們現在就能 mitigate** 的？
> 5. 什麼樣的**早期信號**會告訴我們『失敗模式 X 正在發生』？」

## 進階：Klein 強調的 Q5 — Early Warning Signals

最容易被忽略但最有用的問題：

> **如果失敗模式 X 正在發生，現在會看到什麼徵兆？**

把這些徵兆寫下來，定期檢查。例子：

| 失敗模式 | Early warning signal |
|---|---|
| 「合作者沒交資料」 | 連續 2 週未回信 / dropbox 沒更新 |
| 「設備校準漂移」 | 連續 3 次 calibration 偏離 > 5% |
| 「實驗動物 mortality 上升」 | 一週內 > 2 隻不明原因死亡 |
| 「指導教授對方向有疑慮」 | meeting 頻率下降 / 沒給回饋 |

## Pre-mortem vs Post-mortem

| 維度 | Pre-mortem | Post-mortem |
|---|---|---|
| 時機 | 啟動前 | 結束 / 失敗後 |
| 目的 | 預防 | 學習 |
| 心態 | 假裝已失敗 | 真的失敗了 |
| 工具搭配 | 配合啟動 review | 配合 [[05_5_Whys_Fishbone]] |
| 輸出 | mitigation plan | lessons learned |

## 何時用

- 專案 / 實驗 / 計畫**啟動前 1 週**
- 重大決策（換 lab、換主題、買大型設備）前
- Grant proposal 提交前 2 週
- 一篇 paper submit 前（找 reviewer 會挑的點）
- Code 大型 refactor 前

## 何時不用

- 探索式研究早期（還沒有具體計畫可預判失敗）
- 團隊心理安全感不足時（會變成檢討大會）
- 時間極度緊迫的情境（pre-mortem 至少需 30 分鐘）

## Klein 的關鍵忠告（容易被忽略）

1. **不要邀請大老闆參加**（他們會主導討論，壓制誠實意見）
2. **邀請有失敗經驗的人 + 新進員工**（前者有教訓、後者沒有 group think）
3. **絕對先個別書寫再分享**（從眾效應比想像中強）
4. **不要問「可能會出什麼錯」** — 這是普通風險 review，pre-mortem 的關鍵是**已經失敗**這個前提

## 常見誤用 / 失敗 pattern

| 錯誤 | 修正 |
|---|---|
| 問成「可能會出什麼錯」 | 改成「已經失敗了，原因是什麼」 |
| 跳過個別書寫直接討論 | 強制先寫 2 分鐘 |
| 只列原因沒列 early warning signals | 補上 Q5 — 沒早期訊號等於沒辦法用 |
| 沒對應 mitigation 行動 | 每個 high-risk cause 配一個 action item |
| 半年後沒回頭檢查 | 設定 calendar reminder 每 1–3 個月回看清單 |

## 與其他方法的關係

- **配合 [[01_Heilmeier_Catechism]]**：Heilmeier Q5 (risks) 應該用 pre-mortem 來深挖，不是隨口列幾個
- **配合 [[05_5_Whys_Fishbone]]**：列出失敗原因後，用 fishbone 分類、用 5 Whys 挖到 root
- **配合 [[09_Steelman_Red_Team]]**：red team 是「站在敵人立場攻擊」，pre-mortem 是「站在未來立場逆推」，兩個互補
- **被 advisor-dialogue 使用**：當使用者已經有具體計畫要動手時，必跑一輪 pre-mortem

## 給 learning-notes skill 的應用提示

當使用者帶的是 **「我計畫做 X」** 類型題目（已有具體 plan，不是探索）時：

1. 在筆記末尾必須有一個 **「失敗模式預判 (Pre-mortem)」** section
2. 列出 5 個最可能的失敗原因
3. 對每個失敗原因列出 mitigation action 與 early warning signal
4. 在「下一步」section 必須包含「3 個月後回看 pre-mortem checklist」這個 task
5. 如果使用者 push back 說「不會失敗的」→ 紅旗，他可能沒認真想

## 參考來源

- [Performing a Project Premortem — HBR (Klein, 2007)](https://hbr.org/2007/09/performing-a-project-premortem)
- [Premortem — Gary Klein 官網](https://www.gary-klein.com/premortem)
- [The Pre-Mortem Method — Psychology Today](https://www.psychologytoday.com/us/blog/seeing-what-others-dont/202101/the-pre-mortem-method)
- [Premortem Tool — AHRQ](https://www.ahrq.gov/hai/tools/mvp/modules/cusp/premortem-tool.html)
- Klein G., *Sources of Power: How People Make Decisions* (1998)
- Mitchell, Russo & Pennington (1989) — 原始 prospective hindsight 研究
