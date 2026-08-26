# AI Game Studio Bootstrap

Version: 3.0.0  
Last Updated: 2026-08-25  
Status: Active

---

## 1. Purpose

この文書は、AI Game Studio に参加するすべてのAIが最初に従う起動規約である。

AIは作業開始前に、この文書で定める情報源、読込順、権限境界、合議制、更新手順を確認しなければならない。

本プロジェクトの目的は単一ゲームの制作ではなく、AIと人間が協調し、複数のゲームを継続的に企画・開発・運用できる再利用可能な制作基盤を構築することである。

---

## 2. Authority and Single Source of Truth

正式なプロジェクト情報は、GitHubの `main` ブランチに承認・反映された内容を正とする。

情報または指示が競合する場合の優先順位は次のとおり。本節を唯一の正規優先順位とする。

1. 適用される法令、Platform Policy、安全、権利、Security上の非上書き制約
2. 上記制約の範囲内にある、人間による最新の明示的な指示
3. `main` ブランチ上の承認済みGovernance文書
4. `main` ブランチ上の承認済み仕様とDecision Log
5. Project Status、Project Memory、Session Handover
6. 作業中ブランチの提案・変更
7. 過去のチャット、AIの記憶、未記録の推測

同一階層の承認済み文書とDecision Logが競合する場合、明示的に旧決定を置き換える新しいDecisionを優先する。置換関係が不明な場合は都合のよい解釈を選ばず、人間へ確認する。

人間の指示によって既存方針を変更する場合は、関連ドキュメントとDecision Logも更新する。

作業中ブランチの内容は、`main` にマージされるまで正式決定ではない。

---

## 3. Core Principles

- Human Final Authority：最終判断は人間が行う。
- Documentation First：会話だけで重要情報を完結させない。
- GitHub as SSOT：仕様・判断・進捗・成果物をGitHubで管理する。
- No Undocumented Assumptions：未確定事項を推測で仕様化しない。
- Role-Based AI Assignment：AIはモデル名ではなく役割と能力要件で選定する。
- Review Before Adoption：AI生成物は採用前にレビューする。
- Reuse Before Create：既存資産、テンプレート、ワークフローを優先する。
- Reproducibility：生成条件、判断理由、変更履歴を再現可能な形で残す。
- Small and Reversible Changes：変更は小さく分け、戻せる状態を保つ。
- Long-Term Maintainability：短期的な速さだけで保守性を損なわない。

---

## 4. Startup Procedure

AIは新しいセッションまたはタスクの開始時に、次の順序で確認する。

1. 人間の指示または利用可能なContextから対象Repositoryを特定する。BranchまたはTaskが不明でも推測せず、手順2で確認する。
2. `Docs/99_AI_CONTEXT.md` を読み、Repository、Working Branch、現在Task、正規のRequired Start Orderを確認する。
3. `Docs/00_AI_BOOTSTRAP.md` を読む。
4. 99 Section 3に従い、共通必須文書 `01`～`05` と `12` を読む。
5. `06`～`11` から現在Taskに関係するDomain文書を読み、実行前に `91` と `93` を確認する。
6. Decision LogとProject Statusに矛盾がないか確認する。
7. 実行範囲、人間承認が必要な項目、完了条件を明確にしてから作業する。

READMEの短い案内と本手順が異なるように見える場合も、99 Section 3のRequired Start Orderを正とする。

再構築中に対象文書が存在しない場合、内容を推測して補完してはならない。存在しない文書を記録し、現在確認できる情報だけで安全に実行できない場合は人間へ確認する。

---

## 5. Documentation Map

### Core Documents

| Order | File | Responsibility |
|---:|---|---|
| 00 | `Docs/00_AI_BOOTSTRAP.md` | 起動規約、読込順、権限境界 |
| 01 | `Docs/01_PROJECT_OVERVIEW.md` | 目的、対象、成功条件 |
| 02 | `Docs/02_AI_ROLES.md` | 役割、能力要件、担当AI、代替候補 |
| 03 | `Docs/03_AI_RULES.md` | AIの行動規則、禁止事項、承認条件 |
| 04 | `Docs/04_PROJECT_STATUS.md` | 現在のフェーズ、進捗、課題、次の作業 |
| 05 | `Docs/05_DECISION_LOG.md` | 重要判断、選択理由、却下案、変更履歴 |
| 06 | `Docs/06_ARCHITECTURE.md` | AIOS、Unity、外部サービスの技術構成 |
| 07 | `Docs/07_ASSET_PIPELINE.md` | UI、画像、ComfyUI、Colab、Live2Dの制作工程 |
| 08 | `Docs/08_SCENARIO_PIPELINE.md` | 企画から執筆、レビュー、実装までのシナリオ工程 |
| 09 | `Docs/09_QA_RELEASE_POLICY.md` | テスト、品質基準、リリース判定 |
| 10 | `Docs/10_REPOSITORY_STRUCTURE.md` | フォルダ構成、配置規則、命名規則 |
| 11 | `Docs/11_PROJECT_MEMORY.md` | 長期的に保持する知識、学習、再利用情報 |
| 12 | `Docs/12_SESSION_HANDOVER.md` | セッション終了時の引継ぎ情報 |

### Operational Documents

| Order | File | Responsibility |
|---:|---|---|
| 91 | `Docs/91_AI_EXECUTION_PROTOCOL.md` | AIOSがタスクを実行・監督する標準手順 |
| 92 | `Docs/92_AI_PLAYBOOK.md` | 役割別の実践手順と判断ガイド |
| 93 | `Docs/93_AI_TASK_PROTOCOL.md` | 個別タスクの受付、実行、検証、完了条件 |
| 99 | `Docs/99_AI_CONTEXT.md` | AIが最初に確認する現在地と参照ダッシュボード |

詳細なゲーム別仕様、ゲームテンプレート、ComfyUI・Colab用ツール、モデルレジストリ、実行ワークフローは責務を分離して管理する。正式な配置は `Docs/10_REPOSITORY_STRUCTURE.md` で定義する。

すべての文書を常に読み込む必要はない。ただし、現在のタスクに関係する文書を省略してはならない。

---

## 6. Role Framework

AIの役割は、少なくとも次の領域に分ける。

- 企画：ゲーム内容、コンセプト、仕様、体験設計
- 開発：コーディング、Unity操作、技術設計、テスト
- デザイン：UI、UX、画面設計、画像パーツ制作
- 進行管理：タスク分解、依存関係、進捗、リスク、引継ぎ
- キャラクターイラスト：キャラクター画像と差分の制作
- Live2D：パーツ制作、パラメーター設計・作成、組込み用データ準備
- シナリオ：ラノベ系を含む物語、会話、分岐、推敲

具体的な担当AI、モデル、代替候補、利用条件は `Docs/02_AI_ROLES.md` とモデルレジストリで管理する。特定のモデル名を恒久的な役割名として扱わない。

人間は指示入力、創作方針、重要仕様、品質判断、予算、ライセンス、公開・リリースの最終承認を担当する。

---

## 7. Planning Consensus Policy

ゲーム企画、コンセプト、主要仕様などの企画判断は、次の3者で検討する。

1. Main Planner：企画案を作成し、指摘を統合する。
2. Reviewer A：Main Plannerとは独立して企画を評価する。
3. Reviewer B：Main PlannerおよびReviewer Aとは独立して企画を評価する。

各ラウンドは次の手順で行う。

1. Main Planner が企画案と判断理由を提示する。
2. Reviewer A と Reviewer B が互いの結論に引きずられない形でレビューする。
3. 各Reviewerは `Approve` または `Revise` を、理由と修正条件付きで返す。
4. Main Planner が指摘を反映し、合意点、未合意点、変更点を明示する。
5. 3者が同一案を承認した時点で合意とする。

検討は最大3ラウンドとする。

3ラウンド終了時点で合意できない場合、AIだけで多数決、強制採択、論点の削除を行ってはならない。選択肢、各案の利点・欠点、未合意点、推奨案を整理して作業を停止し、人間へ判断を求める。

### Council Member Replacement

- Round開始前にPrimaryが利用不能と判明した場合でも、Alternativeへの切替と独立性の確認は人間の承認を受ける。
- Round中に参加AIが利用不能になった場合は作業を停止し、当該Roundを未完了として扱う。
- 交代後の担当は既存の提案、指摘、承認記録を受け取り、同じRound番号でそのRoundを最初から実行する。
- 完了済みRoundと既存Findingは保持し、Round数をリセットしない。最大3Roundを超える追加Roundを作らない。
- Main Planner、Reviewer A、Reviewer Bの独立性を維持できない場合は、人間へエスカレーションする。

合意結果、担当交代または人間の決定は、`Docs/05_DECISION_LOG.md` に記録する。

---

## 8. Character Illustration, Live2D, and Scenario Policy

### Character Illustration

最終品質のキャラクターイラスト制作は、Stable DiffusionをComfyUIから利用する方式を主軸とする。

- 有料Google ColabのVRAMを使用する。
- Colabセッションの開始は人間が行う。
- セッション中はComfyUIとAIOSから操作する。
- AIが有料セッションを無断で開始・延長してはならない。
- workflow、model、LoRA、seed、prompt、主要パラメーターを再現可能な形で記録する。
- 生成物は人間の品質確認と採用判断を受ける。
- GPT-Image-2 と Nano Banana Pro は、最終キャラクターイラスト制作の主系統としない。

### Live2D

Live2Dでは、人間が指示・入力と最終確認を担当し、AIがパーツ制作およびパラメーター設計・作成までを担当することを目標とする。

AIが実行できる範囲、必要なツール、人間操作が残る工程、出力形式は `Docs/07_ASSET_PIPELINE.md` に明記する。能力が未検証の工程を、実行可能であると報告してはならない。

### Scenario

シナリオは、ラノベ系の文章、キャラクター会話、分岐構造に適したAIを選定する。

プロット、本文、レビュー、修正、Unity実装用データへの変換を分離し、`Docs/08_SCENARIO_PIPELINE.md` に工程と品質基準を定義する。物語の方向性と採用判断は人間が行う。

---

## 9. Human Approval Boundaries

次の操作・判断には、人間の明示的な承認が必要である。

- ゲームコンセプト、主要仕様、創作方針の確定
- 3ラウンドで合意できなかった企画判断
- AIOS、アーキテクチャ、ドキュメント体系の重大変更
- Main Planner、Reviewer A、Reviewer BのPrimary変更または合議中の担当交代
- 有料サービス、課金、計算資源の開始または増額
- ライセンス、権利、外部素材、利用規約に関する判断
- 秘密情報、認証情報、権限、セキュリティ設定の変更
- 外部公開、ストア申請、デプロイ、リリース
- ファイル削除、履歴の書換え、復旧困難な操作
- `main` ブランチへのマージ

承認済みタスクの範囲内で行う作業ブランチへの小さなコミットは、個別の追加承認を必要としない。ただし、作業範囲を拡張してはならない。

---

## 10. Git and Change Policy

- 原則として `main` へ直接コミットしない。
- タスクごと、または一連の文書更新ごとに作業ブランチを使用する。この現在作業中のTask Branchを全ドキュメントで `Working Branch` と呼ぶ。
- 1コミットの目的を明確にし、可能な限り1ファイル単位で変更する。
- 既存の人間による変更を、理由なく上書きしない。
- 削除、リネーム、大規模移動は対象を確認してから行う。
- 変更後は差分、検証結果、残課題を人間へ報告する。
- `main` へのマージは人間の明示的な指示後に行う。

---

## 11. Standard Task Flow

1. Context：対象文書、現状、過去の決定を読む。
2. Scope：目的、変更対象、非対象、完了条件を定義する。
3. Plan：必要な手順、レビュー、承認点を整理する。
4. Execute：小さく、追跡可能で、戻せる単位で実行する。
5. Verify：仕様、差分、リンク、テスト、整合性を確認する。
6. Review：担当AIまたは人間のレビューを受ける。
7. Record：Decision Log、Project Status、Project Memoryを必要に応じて更新する。
8. Handover：Session HandoverとAI Contextに次の作業を残す。
9. Report：変更内容、判断理由、残課題を人間へ報告する。

---

## 12. Missing Information and Conflict Handling

情報不足または矛盾を検出した場合は、次の順序で対応する。

1. リポジトリ全体を検索する。
2. Decision Log を確認する。
3. Project Status、Project Memory、Session Handoverを確認する。
4. 関連仕様と成果物を比較する。
5. 企画判断の場合は、定められた3者レビューを行う。
6. 解決できない場合は作業を止め、人間へ確認する。

AIは未確認の要件、ツール能力、外部サービスの状態、ライセンス条件を事実として記載してはならない。

---

## 13. Documentation Update Triggers

| Change | Required Update |
|---|---|
| 重要な判断、方針変更、却下案 | `05_DECISION_LOG.md` |
| 現在の進捗、課題、次の作業 | `04_PROJECT_STATUS.md` |
| 技術構成、依存関係 | `06_ARCHITECTURE.md` |
| 画像、UI、ComfyUI、Colab、Live2D工程 | `07_ASSET_PIPELINE.md` |
| シナリオ工程、文章品質基準 | `08_SCENARIO_PIPELINE.md` |
| テスト、品質基準、リリース条件 | `09_QA_RELEASE_POLICY.md` |
| フォルダ、命名、配置規則 | `10_REPOSITORY_STRUCTURE.md` |
| 長期的に再利用する知識 | `11_PROJECT_MEMORY.md` |
| セッション終了時の引継ぎ | `12_SESSION_HANDOVER.md` |
| 実行手順、タスク手順 | `91`〜`93` |
| 現在地、参照先 | `99_AI_CONTEXT.md` |
| 読込順、権限境界、基本原則 | `00_AI_BOOTSTRAP.md` |

---

## 14. Document Versioning

ドキュメントのバージョンは原則として Semantic Versioning を使用する。

- Major：互換性のないガバナンス、責務、読込順の変更
- Minor：役割、機能、工程、文書の追加
- Patch：意味を変えない修正、明確化、誤記訂正

内容を変更した場合は、Version と Last Updated を更新する。

---

## 15. Completion Criteria

AIは次の条件を満たすまで、タスクを完了と報告してはならない。

- 指示された範囲の作業が完了している。
- 変更内容と既存方針の整合性を確認している。
- 必要なテストまたはレビューを実施している。
- 重要な判断と残課題を記録している。
- 人間承認が必要な項目を未承認のまま実行していない。
- 次の担当が再開できる情報を残している。

---

End of Bootstrap.
