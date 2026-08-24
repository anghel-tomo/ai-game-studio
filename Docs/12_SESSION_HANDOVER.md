# Session Handover

Version: 1.0.2  
Last Updated: 2026-08-24  
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

Date: 2026-08-24  
Session / Task ID: DOCS-FOUNDATION-001  
Executor: Codex  
Repository: `anghel-tomo/ai-game-studio`  
Branch: `codex/aios-docs-revision`  
Draft Pull Request: [#1](https://github.com/anghel-tomo/ai-game-studio/pull/1)  
Base Branch: `main`  
Status: READY_FOR_REVIEW / NOT MERGED

### Goal

最終目標として承認された文書構成 `00`～`12`、`91`～`93`、`99` を作成し、AI Game Studioの役割、Pipeline、承認境界、運用方法を整備する。

### Completed

- `00_AI_BOOTSTRAP.md`と`01_PROJECT_OVERVIEW.md`をVersion 2.0.0へ更新
- 最終構成の`02`～`12`を新規作成
- `91_AI_EXECUTION_PROTOCOL.md`を新規作成
- `92_AI_PLAYBOOK.md`を新規作成
- `93_AI_TASK_PROTOCOL.md`を新規作成
- `99_AI_CONTEXT.md`を新規作成
- READMEを最終構成とApache License 2.0へ整合
- 旧番号の`02_AI_RULES.md`、`03_PROJECT_STATUS.md`、`04_SESSION_HANDOVER.md`をDeprecated化
- GitHub上の必須17文書を再取得し、存在とMetadataを確認
- READMEの相対Link 26件を検査し、Broken Link 0件を確認
- 3者合議、Stable Diffusion、Human-Started Colab、Live2D未検証、Scenario方針の横断整合性を確認
- Draft Pull Request [#1](https://github.com/anghel-tomo/ai-game-studio/pull/1)を作成

### Decisions

- D-001～D-013：`Docs/05_DECISION_LOG.md`を参照
- 企画は3者合議、最大3ラウンド
- 本番キャラクターイラストはStable Diffusion + ComfyUI
- 有料Colabは人間がセッション開始
- GPT-Image-2とNano Banana Proは主系統にしない
- AIがLive2Dパーツ・パラメーター作成まで担当する目標
- ラノベ系Scenario Pipeline
- Human Final Authority
- mainへのマージと破壊的操作は人間承認

### Tests / Reviews

- GitHub上の作成結果再取得：実施
- 必須17文書の存在確認：Pass
- Version / Last Updated / Status確認：Pass
- README Link検査：26件、Broken 0件
- License表記：Apache License 2.0へ一致
- Legacy File：3件ともDEPRECATED
- 主要方針横断確認：Pass
- Independent Reviewer AI：未実施
- Unity / Firebase / Colab / Live2D実機Test：文書Taskの範囲外、未実施

### Not Completed

- Independent Reviewer AIによる全体Review
- Review Findingへの対応
- 人間による最終確認
- 旧番号文書の削除判断
- mainへのマージ
- Stage 2以降の実装

### Blockers and Risks

文書作成にBlockerはない。

実装面では、Colab/ComfyUI接続、Unity操作、Live2D自動化、モデル評価が未検証である。

### Human Approval Required

- 旧番号文書の削除
- mainへのマージ
- 有料サービスを用いた実装開始
- 公開・Release

### Next Actions

1. Independent Reviewer AIを決定する。
2. Draft Pull Request #1の17文書とREADMEをReviewさせる。
3. FindingをCritical / Major / Minor / Suggestionへ分類する。
4. 必要な修正を同じBranchへ反映する。
5. 人間が最終差分を確認する。
6. 人間が旧文書削除とmainへのマージを判断する。

### Restart Procedure

1. `Docs/99_AI_CONTEXT.md`を読む。
2. `Docs/00_AI_BOOTSTRAP.md`を読む。
3. Draft Pull Request [#1](https://github.com/anghel-tomo/ai-game-studio/pull/1)を開く。
4. `Docs/04_PROJECT_STATUS.md`と本書を確認する。
5. Independent Reviewから再開する。

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
