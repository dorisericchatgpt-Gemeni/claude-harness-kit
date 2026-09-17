---
title: Steelman + Red Team — 逆向自我攻擊
type: methodology-note
category: argument-validation
created: 2026-05-07
tags: [methodology, critical-thinking, devil-advocate, steelman, red-team]
---

# Steelman + Red Team

## 一句話定義

> **Steelman**: The opposite of strawman — to argue against an opposing position, **first reconstruct it in its strongest possible form**, then refute that.
> **Red Team**: An adversarial group (originally military) tasked to deliberately attack one's own plan / system / argument from the outside, exposing weaknesses before real adversaries do.

中文：**Steelman 是「先把對手立場講到最強再反駁」**，**Red Team 是「自己組一隊扮演敵人來攻擊自己」**。兩者是同一個哲學的個人版與團體版。

## 起源

- **Steelman**：與「strawman fallacy」（稻草人謬誤）相對。「Steel man」一詞在 2010 年代由 rationalist 社群（LessWrong, Slate Star Codex）廣傳，但概念可追溯至 John Stuart Mill *On Liberty* (1859) — 主張「真正理解一個立場，必須能把它講到比支持者本人更好」。
- **Red Team**：軍事用語（冷戰時期 wargame），1990 年代後擴展到 cybersecurity（penetration testing）、business strategy、policy analysis。

## Steelman — 個人實踐

### 核心問題清單

當你不同意一個立場 / 想法 / 論文時：

1. **這個立場的最強版本是什麼？** 比作者本人寫的還強。
2. **支持者最聰明的人會怎麼為它辯護？** 不是 strawman，是 actual best case。
3. **如果我必須說服自己接受這個立場，我會用什麼論證？**
4. **我現在的反對，是針對最強版還是稻草人版？**
5. **重新表述後，我還反對嗎？反對的點是什麼？**

### 例子（你的領域）

你不同意：「我覺得 fMRI 不適合做 BCI 研究」

Steelman 過程：
- 強版重述：「fMRI 雖然 temporal resolution 差（~1 Hz），但它是**唯一**能 non-invasively 全腦 covering 的成像方式。BCI 早期需要全腦 mapping 找 candidate region，這是 single-cell electrophysiology 做不到的。」
- 然後問自己：我反對的是「fMRI 適合做所有 BCI 研究」（強版沒這樣講），還是「fMRI 適合做 closed-loop BCI」（這才是真正的爭點）？
- 結論：我的真正立場是「fMRI 不適合 closed-loop」，不是「fMRI 不適合 BCI」。

→ Steelman 讓你**找到真正的爭點**，避免在稻草人上浪費時間。

### Steelman 的紀律

1. **重述要讓對方點頭**（「對，我就是這個意思」）
2. **可以加入對方沒講的最強論點**（你比作者本人還挺他）
3. **重述完之後再反駁**，不能跳過直接攻擊

## Red Team — 團體實踐

### 核心結構

| 角色 | 任務 |
|---|---|
| **Blue Team** | 提出計畫 / 系統 / 論點的人 |
| **Red Team** | 獨立小組，**任務是找出 Blue Team 的弱點** |
| **White Cell** | 仲裁、設定規則 |

### 操作流程

1. **目標明確**：要 red team 的是計畫？論文？系統？policy？
2. **Red Team 獨立**：不參與 Blue Team 的設計過程，避免污染
3. **時間限制**：給 Red Team 1–4 週深入研究 Blue Team 的方案
4. **完整攻擊**：Red Team 從多角度攻擊：
   - 技術可行性
   - 邏輯漏洞
   - 隱藏假設
   - 競爭者反應
   - Worst case scenarios
   - Adversarial inputs
5. **書面 report**：Red Team 寫完整報告，Blue Team 必須**逐點回應**
6. **整合**：Blue Team 修改方案，公開哪些點吸納、哪些拒絕（含理由）

### 核心問題清單（Red Team 提問模板）

當你扮演 Red Team 攻擊一個方案時：

1. **隱藏假設**：作者假設了什麼**沒明說**的東西？這些假設如果錯了會怎樣？
2. **最壞情境**：什麼樣的世界 / 競爭者 / 敵人會讓這個方案徹底失敗？
3. **Adversarial input**：如果一個聰明且有惡意的人故意操作系統 / 數據，會怎樣？
4. **時間視角**：5 年後 / 10 年後這個方案還成立嗎？什麼會讓它過時？
5. **二階效應**：這個方案成功之後，**衍生**什麼新問題？
6. **誰會反對**：哪些利害關係人會抵抗？他們會怎麼反擊？
7. **資源 fragility**：依賴哪些外部資源？如果斷供？
8. **替代方案**：如果不做這個，有什麼替代？替代的優劣？

## Steelman vs Red Team 對比

| 維度 | Steelman | Red Team |
|---|---|---|
| 規模 | 個人 | 團體 |
| 目的 | 確保自己的反駁打到實質 | 找出方案的脆弱點 |
| 心態 | 同理 + 反駁 | 對抗 + 攻擊 |
| 適用 | 辯論、寫作、選擇之間 | 大型計畫、安全、策略 |
| 時間 | 數分鐘 | 數天到數週 |

兩者**底層哲學相同**：**主動暴露弱點比被動遭遇弱點便宜得多**。

## 何時用

**Steelman 用於：**
- 寫論文 Discussion 處理 alternative interpretations
- 辯論前準備
- 讀立場與你不同的論文（避免帶有偏見）
- 自我檢查（「我真的理解反方嗎？」）

**Red Team 用於：**
- 大型 grant proposal 提交前
- 重大投資決策
- Cybersecurity penetration testing
- 公開政策設計
- 軍事計畫
- 機器學習系統 deployment 前的 adversarial testing

## 何時不用

- 已經對自己立場 100% 有把握的事實性陳述（「水的沸點是 100°C」）
- 時間極度緊迫
- 純情感 / 美學議題（沒有客觀對錯）
- 早期發想階段（會壓抑創意）

## 常見誤用 / 失敗 pattern

| 錯誤 | 修正 |
|---|---|
| Steelman 只是稻草人換個包裝 | 重述後問自己「對方會點頭嗎？」 |
| Red Team 跟 Blue Team 太親近 | Red Team 必須獨立招募，不參與設計 |
| Red Team 只挑小毛病 | 強制針對「策略級弱點」、「致命假設」 |
| Blue Team 不真誠回應 | 規定逐點書面回應，否則沒效 |
| 沒有 White Cell 仲裁 | 沒有第三方會變成情緒戰 |
| Red Team 報告做完就丟 | 必須整合進新版方案、追蹤吸納率 |

## 與其他方法的關係

- **配合 [[06_Pre_mortem]]**：Pre-mortem 是「假設未來失敗」，Red Team 是「現在主動攻擊」，兩個搭配最強
- **配合 [[08_Toulmin_Argumentation]]**：Steelman 重述對方的 claim + warrant + grounds 到最強再反駁
- **配合 [[12_Popper_Falsifiability]]**：Red Team 攻擊 = 主動尋找 falsification 條件
- **配合 [[07_Socratic_Method]]**：Steelman 用 Socratic 提問「對方最強的論證是什麼？」
- **被 advisor-dialogue 使用**：使用者表達強烈立場時，advisor 主動 steelman 反方

## 給 learning-notes skill 的應用提示

當筆記涉及 **「我認為 X」、「X 比 Y 好」、「應該選 X」** 類結論時：

1. 必須有一個 **「Steelman 反方立場」** section
2. 在這個 section，寫下**反方最強的論證**（不是稻草人）
3. 然後寫使用者**回應反方**的論點
4. 如果是大型計畫類筆記，必須有 **「Red Team 攻擊清單」** section（用 Red Team 8 問模板）
5. 對自己最確定的結論最該做 steelman — 「我為什麼這麼確定？反方會怎麼說？」

## 應用案例

- Antigravity 分析核查表：保留原分析最強洞見，同時核對概念歸屬、硬錯、反例與當代延伸。

## 參考來源

- [Steelman argument — Wikipedia / LessWrong](https://www.lesswrong.com/tag/steelmanning)
- [Red Team — Wikipedia](https://en.wikipedia.org/wiki/Red_team)
- [Red Teaming: How Your Business Can Conquer the Competition — Bryce Hoffman](https://www.brycehoffman.com/red-teaming-book) (2017)
- [The Steel Man Technique — Slate Star Codex](https://slatestarcodex.com/2017/04/27/contra-friedersdorf-on-the-warm-cradle/)
- Mill J.S., *On Liberty* (1859), Chapter II
- *Red Team Handbook* — University of Foreign Military and Cultural Studies, US Army (2012)
