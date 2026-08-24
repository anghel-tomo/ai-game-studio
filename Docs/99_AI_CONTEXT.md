# AI Context

Version: 1.0.2  
Last Updated: 2026-08-24  
Status: Active

---

## 1. Read This First

この文書は、AI Game Studioへ参加するAIが最初に確認する現在地と参照ダッシュボードである。

詳細規則を本書だけで判断せず、必ず `Docs/00_AI_BOOTSTRAP.md` と現在タスクに必要な責任文書を読む。

---

## 2. Current Project State

| Item | Current State |
|---|---|
| Project | AI Game Studio |
| Stage | Stage 1: Governance Foundation |
| Focus | Independent Reviewと人間の最終確認 |
| Repository | `anghel-tomo/ai-game-studio` |
| Default Branch | `main` |
| Working Branch | `codex/aios-docs-revision` |
| Working Branch Status | mainへ未マージ |
| Draft Pull Request | [#1](https://github.com/anghel-tomo/ai-game-studio/pull/1) |
| Implementation Status | 主要フォルダはプレースホルダー。Unity等は未実装 |
| Next Decision | Reviewer Findingへの対応、旧文書削除、mainへのマージ |

---

## 3. Required Start Order

1. `Docs/99_AI_CONTEXT.md`
2. `Docs/00_AI_BOOTSTRAP.md`
3. `Docs/01_PROJECT_OVERVIEW.md`
4. `Docs/02_AI_ROLES.md`
5. `Docs/03_AI_RULES.md`
6. `Docs/04_PROJECT_STATUS.md`
7. `Docs/05_DECISION_LOG.md`
8. `Docs/12_SESSION_HANDOVER.md`
9. 現在Taskに必要なDomain文書
10. `Docs/91_AI_EXECUTION_PROTOCOL.md`
11. `Docs/93_AI_TASK_PROTOCOL.md`
12. Current Task

Role別手順が必要な場合は `Docs/92_AI_PLAYBOOK.md` を読む。

存在しない文書を推測で補完しない。

---

## 4. Confirmed Decisions

- GitHub mainを承認済み情報のSSOTとする。
- 人間が最終判断者である。
- AIはRoleとCapabilityで選定し、特定modelへ恒久固定しない。
- 企画はMain Planner、Reviewer A、Reviewer Bの3者合議とする。
- 合議は最大3ラウンドとし、未合意なら人間へ判断を求める。
- 本番キャラクターイラストはStable Diffusion + ComfyUIを主系統とする。
- 有料Google Colabは人間がセッションを開始する。
- 稼働中のColabをComfyUIとAIOSから操作する。
- GPT-Image-2とNano Banana Proは本番キャラクターの主系統にしない。
- Live2DはAIがパーツ制作とパラメーター設計・作成まで担当することを目標とする。
- Live2D自動化は未検証であり、Human Fallbackを残す。
- シナリオを独立Pipelineとし、ラノベ系文章に適したAIを比較評価する。
- Unity 6、Firebase、WebGL-firstを基本技術方針とする。
- 破壊的操作とmainへのマージは人間承認を必要とする。

詳細は `Docs/05_DECISION_LOG.md` を参照する。

---

## 5. Document Routing

| Task | Read |
|---|---|
| Project Purpose | `01_PROJECT_OVERVIEW.md` |
| AI Assignment / Reviewer | `02_AI_ROLES.md` |
| Permission / Prohibition | `03_AI_RULES.md` |
| Current State / Next Task | `04_PROJECT_STATUS.md` |
| Why a Decision Was Made | `05_DECISION_LOG.md` |
| Unity / Firebase / AIOS | `06_ARCHITECTURE.md` |
| Character / UI / Colab / Live2D | `07_ASSET_PIPELINE.md` |
| Story / Dialogue / Branch | `08_SCENARIO_PIPELINE.md` |
| Test / Release | `09_QA_RELEASE_POLICY.md` |
| File Location / Naming | `10_REPOSITORY_STRUCTURE.md` |
| Durable Knowledge | `11_PROJECT_MEMORY.md` |
| Restart Work | `12_SESSION_HANDOVER.md` |
| Orchestration Lifecycle | `91_AI_EXECUTION_PROTOCOL.md` |
| Role Procedures | `92_AI_PLAYBOOK.md` |
| Individual Task Format | `93_AI_TASK_PROTOCOL.md` |

---

## 6. Current Documentation Status

### New Final Structure

- `00_AI_BOOTSTRAP.md`
- `01_PROJECT_OVERVIEW.md`
- `02_AI_ROLES.md`
- `03_AI_RULES.md`
- `04_PROJECT_STATUS.md`
- `05_DECISION_LOG.md`
- `06_ARCHITECTURE.md`
- `07_ASSET_PIPELINE.md`
- `08_SCENARIO_PIPELINE.md`
- `09_QA_RELEASE_POLICY.md`
- `10_REPOSITORY_STRUCTURE.md`
- `11_PROJECT_MEMORY.md`
- `12_SESSION_HANDOVER.md`
- `91_AI_EXECUTION_PROTOCOL.md`
- `92_AI_PLAYBOOK.md`
- `93_AI_TASK_PROTOCOL.md`
- `99_AI_CONTEXT.md`

### Legacy Files

- `02_AI_RULES.md`
- `03_PROJECT_STATUS.md`
- `04_SESSION_HANDOVER.md`

Legacy Filesは3件ともDeprecated化済みで、新文書への参照だけを残している。削除は人間の明示的な承認後に行う。

---

## 7. Current Capability Status

### Documented / Ready for Review

- Governance
- AI Role Framework
- Three-Party Planning Policy
- Architecture Target
- Asset Pipeline Design
- Scenario Pipeline Design
- QA / Release Policy
- Repository Structure
- Memory / Handover
- Execution / Task Protocol

### Not Implemented or Unvalidated

- Antigravity 2.0によるAIOS自動運用
- Model Registry実File
- Unity Template
- Unity CLI / MCP / Computer Use
- Firebase Project / Secrets / CI
- WebGL自動Build / Deploy
- Colab + ComfyUI接続workflow
- Stable Diffusion model / LoRA選定
- Live2D自動化
- Scenario model評価とUnity変換
- QA自動化
- 最初のGame

目標構成を実装済みと報告しない。

---

## 8. Immediate Next Actions

1. Independent Reviewer AIで17文書とREADMEをReviewする。
2. FindingをSeverity別に整理する。
3. 必要な修正を作業Branchへ反映する。
4. 人間が差分を最終確認する。
5. 人間がLegacy Files削除の要否を判断する。
6. 人間の明示承認後にmainへマージする。
7. Stage 2の最初のTaskを決定する。

---

## 9. Human Approval Pending

- Legacy Filesの削除
- mainへのマージ
- 有料Colabを用いた実装開始
- Unity、Firebase、Live2D等の外部接続・設定
- Public Deploy / Release

---

## 10. Session Update Rule

セッション終了時に次を更新する。

- Stage、Focus、Branch
- Completed / Not Implemented
- Immediate Next Actions
- Human Approval Pending
- `04_PROJECT_STATUS.md`
- `12_SESSION_HANDOVER.md`

重要な判断は本書へ直接詳細を書かず、Decision Logを更新して参照する。

---

End of AI Context.
