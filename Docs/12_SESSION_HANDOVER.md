# Session Handover

Version: 1.0.0  
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

### Restart Procedure

次担当が最初に読む文書、取得するBranch、実行する確認を順番に記載する。

---

## 5. Current Handover

Date: 2026-08-24  
Session / Task ID: DOCS-FOUNDATION-001  
Executor: Codex  
Repository: `anghel-tomo/ai-game-studio`  
Branch: `codex/aios-docs-revision`  
Base Branch: `main`  
Status: IN_PROGRESS / NOT MERGED

### Goal

最終目標として承認された文書構成 `00`～`12`、`91`～`93`、`99` を作成し、AI Game Studioの役割、Pipeline、承認境界、運用方法を整備する。

### Completed

- `00_AI_BOOTSTRAP.md`をVersion 2.0.0へ更新
- `01_PROJECT_OVERVIEW.md`をVersion 2.0.0へ更新
- `02_AI_ROLES.md`を新規作成
- `03_AI_RULES.md`を新規作成
- `04_PROJECT_STATUS.md`を新規作成
- `05_DECISION_LOG.md`を新規作成
- `06_ARCHITECTURE.md`を新規作成
- `07_ASSET_PIPELINE.md`を新規作成
- `08_SCENARIO_PIPELINE.md`を新規作成
- `09_QA_RELEASE_POLICY.md`を新規作成
- `10_REPOSITORY_STRUCTURE.md`を新規作成
- `11_PROJECT_MEMORY.md`を新規作成
- `12_SESSION_HANDOVER.md`を新規作成

### Confirmed Decisions

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
- Metadata確認：実施
- 文書間リンク全件検査：Operational Documents作成後に実施予定
- Independent Reviewer AI：未実施
- Unity / Firebase / Colab / Live2D実機Test：未実施

### Not Completed

- `91_AI_EXECUTION_PROTOCOL.md`
- `92_AI_PLAYBOOK.md`
- `93_AI_TASK_PROTOCOL.md`
- `99_AI_CONTEXT.md`
- README更新
- 旧番号文書のDeprecated化
- 全文書の自動整合性確認
- Independent Reviewer AIによる最終Review
- mainへのマージ

### Blockers and Risks

文書作成にBlockerはない。

実装面では、Colab/ComfyUI接続、Unity操作、Live2D自動化、モデル評価が未検証である。

### Human Approval Required

- 旧番号文書の削除
- mainへのマージ
- 有料サービスを用いた実装開始
- 公開・Release

### Next Actions

1. Operational Documentsを作成する。
2. READMEと旧文書を整合させる。
3. 全文書のリンク、Version、用語を検査する。
4. Independent Reviewer AI候補を提示する。
5. 人間が確認後、修正またはmainへのマージを判断する。

### Restart Procedure

1. `Docs/99_AI_CONTEXT.md`を読む。未作成の場合は本書を読む。
2. `Docs/00_AI_BOOTSTRAP.md`を読む。
3. `codex/aios-docs-revision`の最新Commitを取得する。
4. `Docs/04_PROJECT_STATUS.md`と本書を確認する。
5. Not Completedの先頭から再開する。

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
