# Session Handover

Version: 1.3.0  
Last Updated: 2026-08-26  
Status: Active

---

## 1. Purpose

本書は、AIまたは人間がセッションを終了する時に、次の担当が安全に作業を再開できる情報を残すための標準形式を定義する。

チャット履歴だけを引継ぎとして扱わない。

---

## 2. Handover Principles

- 実行済みと未実行を分離する。
- 作業Branch、Commit、変更Fileを記載する。
- 決定、提案、未承認を区別する。
- 失敗、Blocker、未検証範囲を隠さない。
- 次の作業を実行可能な単位で記載する。
- Secrets、token、個人情報を記載しない。
- Status、Decision Log、Project Memory、AI Contextと矛盾させない。
- mainへ未反映の場合は明記する。

---

## 3. Required Handover Format

```markdown
# Session Handover

Date:
Session / Task ID:
Executor:
Repository:
Branch:
Pull Request:
Base Commit:
Latest Commit:
Status:

## Goal

## Completed

## Changed Files

## Decisions

## Tests / Reviews

## Not Completed

## Blockers and Risks

## Human Approval Required

## Next Actions

## Restart Procedure

## References
```

---

## 4. Field Rules

### Goal

セッション開始時に依頼された目的を記載する。途中で拡張された場合は、追加指示を分けて記載する。

### Completed

実際に完了し、再取得またはEvidenceで確認できる内容だけを書く。

### Changed Files

Fileごとに変更目的を1行で記載する。CommitまたはPull Requestへ対応付ける。

### Decisions

新しい決定はDecision LogのIDを参照する。未承認案をDecisionとして記載しない。

### Tests / Reviews

実行したTest、Review、Link Check、Buildを記載する。実行していない場合はNot Runとする。

### Not Completed

予定していたが実行していない内容を記載する。次担当がCompletedと誤解しないようにする。

### Blockers and Risks

権限、情報、環境、能力、費用、権利、外部接続の問題を記載する。

### Human Approval Required

削除、mainへのマージ、有料処理、公開等の承認待ちを記載する。

### Next Actions

次担当がそのままTask化できる順序で記載する。

### Restart Procedure

次担当が最初に読む文書、取得するBranch、実行する確認を順番に記載する。

---

## 5. Current Handover

Date: 2026-08-26  
Session / Task ID: DOCS-FOUNDATION-004  
Executor: Codex  
Repository: `anghel-tomo/ai-game-studio`  
Working Branch: `codex/aios-docs-revision`  
Draft Pull Request: [#1](https://github.com/anghel-tomo/ai-game-studio/pull/1)  
Base Branch: `main`  
Status: HUMAN_APPROVED / MERGE_AND_CLEANUP_AUTHORIZED / NOT_MERGED

### Goal

人間の最終承認をDecision Logへ記録し、Pull Request #1を`main`へマージした後、Legacy Filesを別のCleanup Pull Requestで削除する。

### Completed

- Claude FreeでGovernance、Pipeline、全体整合性の3回Reviewと、修正後1回のFocused Independent Re-reviewを実施
- R1・R2・R3のFindingを実際の作業Branchと既決定事項へ照合
- 企画人数はMain Planner 1名 + Reviewer 2名 = 合計3者で正しいことを再確認
- 誤認、重複、Review時点差をD-014へ分類
- 読込順とInstruction Priorityを正規化
- 全RoleのHuman Fallback、合議中の交代Rule、Primary変更の人間承認を追加
- Pilot期間の暫定OrchestratorとRelease Coordinator案をD-015へ記録
- Asset / Scenario Manifest、Colab Secret受け渡し、Session監視、Checkpointを明確化
- Character同一性ChecklistとStatic Validationを追加
- 91 / 93のTask Stateを統一し、Task ID形式を実態へ整合
- Project Status、Decision Log、Session Handover、AI ContextをReview後の状態へ同期
- `REVIEW_04`で既存24件がFIXEDまたはPARTIALLY_FIXED、新規Critical / Majorが0件、新規Minorが3件と確認
- R4-001～R4-003を反映し、R1-005の残課題を含む3件を解消
- 修正箇所をGitHubから再取得し、15 / 15項目の機械確認がPass
- D-014・D-015を人間承認済みとして記録
- Review原文の非保存、Pull Request #1のマージ、Legacy Files削除をD-016として記録

### Decisions

- D-001～D-013：既存の承認済みDecision
- D-014：Review Finding採否と修正方針、ACCEPTED
- D-015：Pilot期間の暫定OrchestratorとRelease Coordinator、ACCEPTED
- D-016：Review記録、Legacy Files削除、main統合方針、ACCEPTED

### Tests / Reviews

- Claude Free Independent Review：初回3回 + Focused Re-review 1回、計4回実施
- CodexによるFindingとGitHub作業Branchの再照合：実施
- 誤認除外：R2-011、R3-006、R3-008
- 時点差として再分類：R3-001
- 修正後のFocused Independent Re-review：実施、Critical / Major 0件
- R4-001～R4-003反映後の再取得確認：15 / 15項目Pass
- Unity / Firebase / Colab / Live2D実機Test：文書Taskの範囲外、未実施

### Not Completed

- Pull Request #1の`main`へのマージ
- Legacy Files 3件の削除とCleanup Pull Requestのマージ
- Stage 2以降の実装

### Blockers and Risks

文書修正にBlockerはない。

実装面では、Colab/ComfyUI接続、Unity操作、Live2D自動化、モデル評価が未検証である。D-014～D-016は人間承認済みだが、現在はまだ`main`へ未反映である。

### Human Approval Required

現在の文書Taskに必要な承認は取得済み。以下の将来操作は別途承認を必要とする。

- 有料サービスを用いた実装開始
- 公開・Release

### Next Actions

1. Pull Request #1を`main`へマージする。
2. `main`上のLegacy Filesと参照を確認する。
3. 別のCleanup Pull RequestでLegacy Files 3件を削除し、検証後に`main`へマージする。
4. Stage 2の最初の実装Taskを決定する。

### Restart Procedure

1. `Docs/99_AI_CONTEXT.md`を読む。
2. `Docs/00_AI_BOOTSTRAP.md`を読む。
3. Draft Pull Request [#1](https://github.com/anghel-tomo/ai-game-studio/pull/1)を開く。
4. `Docs/04_PROJECT_STATUS.md`、`Docs/05_DECISION_LOG.md`のD-014・D-015、本書を確認する。
5. Pull Request #1のマージから再開する。

---

## 6. Session End Update

セッション終了前に次を更新する。

- `04_PROJECT_STATUS.md`
- `05_DECISION_LOG.md`：新しい重要判断がある場合
- `11_PROJECT_MEMORY.md`：永続的な学習がある場合
- `12_SESSION_HANDOVER.md`
- `99_AI_CONTEXT.md`

---

End of Session Handover.
