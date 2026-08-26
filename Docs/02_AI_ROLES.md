# AI Roles

Version: 2.0.1  
Last Updated: 2026-08-26  
Status: Active

---

## 1. Purpose

本書は、AI Game Studioで必要となる役割、責任、能力要件、現行候補、代替手段を定義する。

役割は恒久的なモデル名ではなく、必要な能力によって定義する。モデル、サービス、料金、利用条件が変わった場合でも、役割と成果物の契約を維持したまま担当を交換できる構造とする。

---

## 2. Role Assignment Principles

- 1つのAIに企画、実装、承認を集中させない。
- 重要な成果物は、作成者とは異なるAIまたは人間がレビューする。
- 役割ごとにPrimary、Alternative、Human Fallbackを持つ。
- Preview、Experimental、外部サービスは利用前に可用性と条件を確認する。
- 担当AIが利用不能でも、タスク、入力、成果物、判断履歴をGitHubから引き継げる状態にする。
- AIの自己申告だけで能力を認定しない。代表タスクによる評価を行う。
- 現行候補はモデルレジストリで更新し、本書の役割定義を頻繁に変更しない。

---

## 3. Human Project Owner

人間はプロジェクトの最終責任者であり、次を担当する。

- AIへの指示入力と優先順位
- ゲームコンセプト、創作方針、主要仕様の最終決定
- AI生成物の採用・不採用
- 予算、有料サービス、ライセンス、権利の判断
- Colabセッションの開始
- セキュリティ、公開、リリース、mainへのマージ承認
- AIだけでは解決できない問題の裁定

AIは人間の最終責任を代替しない。

---

## 4. Current Role Map

現行候補は暫定構成であり、このRole Mapは2026-08-26に改訂した。各Candidateの利用時にはモデルレジストリのTerms Last Verifiedと公式情報、実環境での利用可否を再確認する。

| Role | Main Responsibility | Current Primary Candidate | Alternative | Human Fallback | Status |
|---|---|---|---|---|---|
| AIOS Orchestrator | タスク分解、割当、実行監督、記録、引継ぎ | Google Antigravity 2.0 | Codex Work + GitHub | Human Project Ownerが手動でOrchestrator手順を実行または委任 | Pilot |
| Producer / Main Planner | 企画統合、仕様整理、優先順位、意思決定案 | GPT-5.6 Sol | Claude Opus 5 | Human Project Owner | Active Candidate |
| Planning Reviewer A | プレイヤー価値、独自性、UX、物語・キャラクター整合性 | Claude Opus 5 | Claude Fable 5 | Human Project Ownerが独立したCreative Reviewerを指名。確保できなければ停止 | Active Candidate |
| Planning Reviewer B | 技術実現性、費用、工数、保守性、リスク | Gemini 3.1 Pro | 人間が指名した独立Feasibility Reviewer | Human Project Ownerが独立した技術・制作Reviewerを指名。確保できなければ停止 | Preview Candidate |
| Architect | システム設計、依存関係、拡張性、設計レビュー | Claude Opus 5 | GPT-5.6 Sol | 人間のTechnical Leadまたは外部専門家 | Active Candidate |
| Developer | コード、Git、テスト、リファクタリング | Codex / GPT-5.6 Sol | Antigravity Agent | 人間のDeveloper | Active Candidate |
| Unity Operator | Unity編集、実行、ビルド、画面確認 | Antigravity 2.0 | Codex + Unity CLI/MCP | 人間のUnity Operator | Capability Validation Required |
| UI/UX Designer | 画面構成、導線、ワイヤー、UIパーツ | Stitch + reasoning model | Figma系ツール + GPT-5.6 | 人間のUI/UX Designer | Pilot |
| Project Manager | タスク、依存関係、進捗、リスク、引継ぎ | GPT-5.6 Terra | GPT-5.6 Sol | Human Project Owner | Active Candidate |
| Researcher | 公式仕様、API、規約、比較調査 | Gemini Deep Research | GPT-5.6 Sol + web research | 人間が公式情報を確認 | Active Candidate |
| Character Illustrator | キャラクター本番画像、差分、再現可能な生成 | Stable Diffusion + ComfyUI | 個別評価した互換workflow | 人間のIllustrator / Art Director | Pipeline Required |
| Live2D Pipeline Agent | パーツ制作、パラメーター案・作成、データ準備 | ComfyUI/SAM系処理 + Cubism連携手段 | 人間による補正・手動作業 | 人間のLive2D Modeler | Unvalidated |
| Scenario Writer | ラノベ系プロット、本文、会話、分岐、推敲 | Claude Opus 5 | GPT-5.6 Sol | 人間のScenario Writer / Editor | Evaluation Required |
| QA Reviewer | 仕様適合、回帰、UX、文書・実装整合性 | 実装担当と異なる上位モデル | 人間レビュー | Human Project Ownerが独立QA担当を指名 | Required |
| Release Coordinator | リリース候補整理、チェック、変更履歴 | Project Manager | 検証済みAIOS Release Workflow | Human Project Owner | Human Approval Required |

Human Fallbackは自動的な権限移譲ではない。PrimaryとAlternativeが利用不能、未検証または独立性を満たさない場合、TaskをBLOCKEDにし、Human Project Ownerが担当者を明示する。必要な専門性を持つ人間を確保できない場合は作業を停止する。

AIOS OrchestratorがPilotの間は、Human Project OwnerがOrchestrator機能を手動実行またはProject Managerへ明示委任する。Release CoordinatorはProject Managerを実行主体とし、自動化検証後のみAIOS Release Workflowへ切り替える。

モデル名は役割名ではない。Current Primary Candidateは、評価時点の候補を示すだけであり、恒久的な採用を意味しない。

---

## 5. Planning Council

企画判断は、Main Planner、Reviewer A、Reviewer Bの3者で行う。

### Main Planner

- 目的、対象ユーザー、体験、制約を整理する。
- 企画案と判断理由を提示する。
- 2名のレビューを統合し、変更点と未合意点を明示する。
- Reviewerの指摘を無断で削除しない。

### Reviewer A: Player and Creative Review

- 面白さ、分かりやすさ、継続動機を評価する。
- UI・UX、キャラクター、世界観、シナリオの一貫性を評価する。
- 既視感、弱い訴求、プレイヤー負担を指摘する。
- Main Plannerとは独立してApproveまたはReviseを返す。

### Reviewer B: Feasibility and Risk Review

- Unityでの実装可能性、技術依存、性能を評価する。
- 制作費、外部サービス費、工数、運用負担を評価する。
- 権利、セキュリティ、保守性、スケジュール上のリスクを指摘する。
- Main PlannerおよびReviewer Aとは独立してApproveまたはReviseを返す。

3者が同一案を承認した場合のみ合意とする。最大3ラウンドで合意できない場合は、論点と選択肢を整理し、人間へ判断を求める。

参加AIの切替は人間承認を必要とする。合議中に交代する場合、完了済みRoundと既存Findingを保持し、未完了Roundを同じRound番号で再実行する。Round数をリセットせず、独立性を維持できなければ人間へエスカレーションする。詳細は `Docs/00_AI_BOOTSTRAP.md` Section 7に従う。

---

## 6. Development Roles

### Architect

Architectは実装前に、構成、責務、依存関係、拡張点、障害時の復旧方法を定義する。

大規模な設計変更は、Developerが単独で決定してはならない。Architectレビューと人間承認を受け、Decision Logへ記録する。

### Developer

Developerは承認された仕様と設計に基づき、コード、テスト、設定、技術文書を変更する。

- 作業ブランチを使用する。
- 理解できないコードを採用しない。
- 変更範囲を必要最小限にする。
- テスト結果と未検証項目を報告する。
- 自分の実装を最終承認しない。

### Unity Operator

Unity Operatorは、Unityプロジェクトを実際に開き、編集、実行、ビルド、画面確認を行える環境を必要とする。

CLI、MCP、Computer Useなどの操作経路は、代表タスクで検証してからActiveへ変更する。接続できない場合は、実行したと報告せず、人間操作用の手順と確認項目を出力する。現在の未検証範囲は `Docs/06_ARCHITECTURE.md` Section 14を正とする。

---

## 7. Creative Roles

### UI/UX Designer

- ユーザーフロー、情報設計、画面構成、操作負担を設計する。
- ワイヤーフレームと実装用仕様を分離する。
- 見た目だけでなく、状態、例外、入力方法、アクセシビリティを定義する。
- 最終デザインは人間の承認を受ける。

### Character Illustrator

本番のキャラクターイラストはStable Diffusion + ComfyUIを主系統とする。

GPT-Image-2とNano Banana Proは、本プロジェクトで求める最終キャラクター品質に達していないため、主系統へ採用しない。

Illustratorは、workflow、model、LoRA、seed、prompt、主要パラメーター、入力画像、出力履歴を記録する。

### Live2D Pipeline Agent

目標範囲は、パーツ制作とパラメーター設計・作成までである。人間は指示・入力と最終確認を担当する。

現時点では完全自動化を検証済みとは扱わない。工程ごとに次を記録する。

- AIが実行可能な操作
- 人間操作が必要な操作
- 入出力形式
- 品質確認方法
- 再実行方法

### Scenario Writer

- 企画意図とキャラクター設定からプロットを作る。
- ラノベ系の読みやすさ、会話の自然さ、キャラクター差を重視する。
- プロット、本文、校正、実装用データ変換を分離する。
- 重要な物語方向と採用本文は人間の承認を受ける。
- モデル選定は代表サンプルによるブラインド評価で決める。

---

## 8. QA and Review Independence

QA Reviewerは、可能な限り成果物の作成者と異なるモデル系統を使用する。

推奨する分離例：

- GPT系が企画を作成した場合、Claude系とGemini系がレビューする。
- GPT系がコードを実装した場合、Claude系が設計・差分レビューする。
- Claude系がシナリオを作成した場合、GPT系が設定・構成・矛盾を検査する。
- 画像生成workflowの作成者とは別の担当が、再現性と権利情報を確認する。

同一モデルを使用する場合は、会話を分離し、元の自己評価を引き継がない独立レビューとして実行する。

---

## 9. Model Registry Requirements

モデルレジストリには、最低限次を記録する。

| Field | Description |
|---|---|
| Role | 担当可能な役割 |
| Provider / Model | 提供元と正確なモデル名 |
| Status | Active / Candidate / Preview / Deprecated / Blocked |
| Strengths | 評価済みの強み |
| Limitations | 制約、不得意、禁止用途 |
| Input / Output | 対応形式と上限 |
| Tool Access | GitHub、web、Unity、画像、外部サービス |
| Cost Class | Free / Low / Medium / High / Human-Started |
| Terms Checked | 規約確認日 |
| Evaluation | 代表タスク、結果、比較対象 |
| Fallback | 利用不能時の代替 |
| Last Verified | 最終確認日 |

Primaryを変更する場合は、事前に人間の明示承認を受け、評価結果と変更理由をDecision Logへ記録する。Planning CouncilのPrimary変更または合議中の担当交代は、独立性への影響も記録する。

---

## 10. Capability Validation

CandidateをActiveへ変更する前に、少なくとも次を確認する。

1. 実際の入力と成果物形式を処理できる。
2. 必要なツールへ承認された方法で接続できる。
3. 代表タスクを再現可能に完了できる。
4. 費用と処理時間が許容範囲である。
5. 権利、利用規約、データ取扱いを確認している。
6. 別担当が成果物をレビューしている。
7. 失敗時のFallbackが用意されている。
8. 認証情報を必要とする接続では、秘密値をChat、GitHub、Notebook出力、Task Packet、Execution Logへ残さない受け渡し・失効手順を検証している。

---

## 11. Escalation

次の場合は、人間へエスカレーションする。

- 企画が3ラウンドで合意しない。
- AI間で事実認識が一致しない。
- 必要な能力が未検証である。
- 有料サービス、権利、公開、セキュリティ判断が必要である。
- 仕様と既存決定が矛盾している。
- 失敗が繰り返され、同じ方法で改善しない。
- 人間の意図を複数に解釈でき、結果が大きく変わる。

---

End of AI Roles.
