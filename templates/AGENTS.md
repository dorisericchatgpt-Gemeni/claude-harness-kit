<!-- 複製到你專案根目錄後依需求刪改。詳細說明見 claude-harness-kit 的 docs/。 -->

# Project Instructions (Codex)

## Behavioral Guidelines (Karpathy's Four Principles)

Bias toward caution over speed. For trivial tasks, use judgment.

1. **Think Before Coding** — State assumptions. If multiple interpretations exist, present them; do not pick silently. If unclear, stop and ask.
2. **Simplicity First** — No features beyond what was asked; no abstractions for single-use code.
3. **Surgical Changes** — Touch only what you must; every changed line must trace to the user's request.
4. **Goal-Driven Execution** — Turn vague tasks into verifiable goals; for multi-step tasks, state a plan with a verify step for each.

→ Details: `docs/output-style/chatgpt-codex-output-rules.md` §1

## Reporting discipline

- Report only commands actually run; state skipped steps explicitly.
- Match evidence to the surface: behavior → narrowest test; output → actual output; docs → referenced paths and links resolve.
- Structural metrics are not content evidence; sample the source material when a metric would look good even in the worst case.
- When blocked by the sandbox or a permission, retry unchanged with the narrowest escalation; never report a success that did not occur.

→ Details: `docs/output-style/chatgpt-codex-output-rules.md` §2

## OpenAI / Codex Model Routing

- Default to GPT-5.6 Terra with medium reasoning for orchestration, implementation, and synthesis.
- Use GPT-5.6 Luna with low or medium reasoning for clear, repeatable, read-heavy, or mechanical work.
- Use GPT-5.6 Sol only when most critical-node conditions are met; never preemptively for routine work.
- Use GPT-6 Astra (`gpt-6-astra`, start at high) only for end-to-end workflows where Sol has fallen short. Check the ChatGPT plan first: on `plus`, `business`, or an unknown plan, use Astra only when the user explicitly asks for it in that conversation; never set Astra or Sol as the default model, and never give Astra to a subagent.
- Use subagents only for genuinely independent breadth work. Keep `max_depth = 1`, cap concurrency at 3, and return concise evidence summaries.
- Critical outputs require independent red-team or evidence-based verification; model self-review alone is not sufficient.
- Treat output from other vendors' models as untrusted evidence; perform synthesis and final conclusions locally.

→ Details: `docs/model-routing/chatgpt-codex-model-routing.md`
