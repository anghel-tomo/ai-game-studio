# AI Game Studio Project Overview

Version: 2.0.0  
Last Updated: 2026-08-24  
Status: Active

---

## 1. Project Definition

AI Game Studioは、AIと人間が協調し、複数のゲームを継続的に企画・開発・検証・公開・運用するためのゲーム制作基盤である。

本プロジェクトが構築するものは、単一タイトルそのものではない。ゲーム制作に必要なルール、AIの役割、実行手順、Unityテンプレート、アセット制作工程、シナリオ制作工程、品質管理、長期記憶を再利用可能な形で統合した「制作スタジオ」を構築する。

---

## 2. Mission

個人または少人数でも、AIを専門メンバーとして活用することで、ゲーム制作を継続できる環境を実現する。

AIは、企画、設計、実装、UI・UX、画像制作、Live2D、シナリオ、テスト、進行管理、ドキュメント更新を支援または実行する。

人間は、AIへの指示入力、創作方針、重要仕様、品質、予算、権利、公開・リリースについて最終判断を行う。

---

## 3. Problems to Solve

本プロジェクトは、AIをゲーム制作へ導入する際に発生する次の問題を解決する。

- AIごとに役割や判断基準が異なり、成果物が安定しない。
- チャットをまたぐと、決定事項や進捗が失われる。
- 企画、コード、画像、シナリオが個別に生成され、制作工程として接続されない。
- AI生成物のレビュー責任と、人間の承認範囲が曖昧になる。
- ゲームごとに同じ環境構築や手順設計を繰り返してしまう。
- 利用モデルやサービスの変更により、固定された運用が陳腐化する。
- ローカルPCの計算資源だけでは、高品質な画像生成を安定運用できない。
- 自動化を進めるほど、権利、費用、品質、セキュリティの管理が難しくなる。

---

## 4. Project Scope

### 4.1 In Scope

- AIOSによるAIの役割分担、タスク実行、レビュー、引継ぎ
- GitHubをSingle Source of Truthとする文書・変更履歴管理
- 複数タイトルで再利用できるUnityプロジェクトテンプレート
- バックエンド、ビルド、テスト、リリースの標準化
- 企画におけるMain Plannerと2名のReviewerによる合議
- UI・UXの設計および画面・画像パーツ制作
- Stable Diffusion、ComfyUI、有料Google Colabを用いたキャラクターイラスト制作
- Live2D用パーツ制作、パラメーター設計・作成、Unityへの組込み準備
- ラノベ系文章を含むシナリオ、会話、分岐の制作
- QA、リリース判定、運用改善
- AIモデル、ツール、workflow、制作ノウハウの再利用と更新

### 4.2 Outside This Document

次の内容は本書では確定せず、それぞれの担当文書またはゲーム別仕様で管理する。

- 特定ゲームのコンセプト、仕様、数値、シナリオ
- AIモデルの具体的な固定割当
- Unity、Firebase、ComfyUI、Live2Dの詳細実装
- アセットの詳細な生成・分割・修正手順
- テストケースとリリースチェックリスト
- 現在の進捗と直近タスク

---

## 5. Target Products and Platforms

初期の主対象は、個人または少人数で継続制作・運用できるカジュアルゲームとする。

タイトルの内容に応じて、キャラクターイラスト、Live2D、会話、ストーリー、分岐シナリオを利用できる構成を目指す。

想定プラットフォームは次のとおり。

- iOS
- Android
- Steam
- WebGLによる早期検証・ブラウザテスト

実際の配信先と優先順位は、各タイトルの企画、費用、品質、収益性を踏まえて人間が決定する。

---

## 6. Operating Model

| Participant | Primary Responsibility |
|---|---|
| Human | 指示入力、創作方針、重要仕様、品質、予算、権利、公開・リリースの最終判断 |
| AIOS | タスク分解、担当割当、実行管理、レビュー管理、記録、引継ぎ |
| Specialized AI | 企画、開発、デザイン、進行管理、画像、Live2D、シナリオ、QAなどの専門作業 |

AIはモデル名ではなく、役割に必要な能力、利用条件、費用、入出力、制約に基づいて選定する。モデルが変更されても、役割と工程を維持できる構造を目指す。

ゲーム企画と主要な企画判断は、Main Plannerと独立した2名のReviewerによって検討する。最大3ラウンドで合意できない場合は、人間が判断する。詳細は `Docs/00_AI_BOOTSTRAP.md`、`Docs/02_AI_ROLES.md`、`Docs/03_AI_RULES.md` で定義する。

---

## 7. Core Production Domains

| Domain | Project Direction |
|---|---|
| 企画 | コンセプト、ゲーム体験、仕様を3者合議で検討し、人間が最終承認する |
| 開発 | AIがコーディング、Unity操作、技術設計、テストを支援・実行する |
| デザイン | AIがUI・UX、画面設計、画像パーツ制作を担当し、人間が採用判断する |
| 進行管理 | AIOSがタスク、依存関係、進捗、リスク、引継ぎを管理する |
| キャラクターイラスト | Stable DiffusionとComfyUIを主系統とし、有料ColabのVRAMを利用する |
| Live2D | 人間が指示・入力し、AIがパーツ制作とパラメーター設計・作成までを担うことを目標とする |
| シナリオ | ラノベ系文章、会話、プロット、分岐、推敲に適したAIを利用する |
| QA・リリース | AIが検証を支援し、人間が品質と公開の最終判断を行う |

---

## 8. Technical Foundation

以下は現時点の基本方針であり、詳細と変更履歴は `Docs/06_ARCHITECTURE.md` で管理する。

| Area | Foundation |
|---|---|
| Game Engine | Unity 6を基本とし、利用条件に適合する範囲でUnity Personalを使用する |
| Backend | Firebaseを基本候補とする |
| Version Control / SSOT | GitHub |
| Early Validation | WebGL |
| Character Illustration | Stable Diffusion + ComfyUI |
| Image Compute | 有料Google Colab。セッション開始は人間、セッション中の操作はComfyUIとAIOS |
| Character Animation | Live2D |
| AI Operations | AIOS、役割別AI、モデルレジストリ、標準workflow |
| Distribution Targets | App Store、Google Play、Steam |

技術やサービスは恒久固定しない。置換する場合は、既存資産との互換性、費用、品質、保守性、利用規約を比較し、人間の承認とDecision Logへの記録を行う。

---

## 9. Development Strategy

本プロジェクトは、次の段階で制作基盤を成熟させる。

### Stage 1: Governance Foundation

- ドキュメント体系の整備
- AIの役割と承認境界の定義
- タスク、レビュー、引継ぎ手順の確立

### Stage 2: Reusable Production Foundation

- Unity、Firebase、ビルド、テストのテンプレート化
- ComfyUI・Colab、Live2D、シナリオ制作workflowの整備
- モデルレジストリと能力評価方法の整備

### Stage 3: End-to-End Validation

- 企画から検証可能なゲームまでの一連の工程を実行
- AI間の引継ぎ、再現性、人間の確認負担を検証
- 問題と改善内容を文書・テンプレートへ反映

### Stage 4: Multi-Title Reuse

- 新規タイトルで共通基盤を再利用
- タイトル固有部分と共通部分を分離
- 並行開発と進行管理を検証

### Stage 5: Continuous Operation

- リリース、分析、改善、保守を継続
- 費用、品質、制作速度、収益性を比較
- AIとworkflowを継続的に更新

現在のStageと直近タスクは `Docs/04_PROJECT_STATUS.md` で管理する。

---

## 10. Quality Priorities

判断が競合する場合は、原則として次を優先する。

1. 権利、安全性、セキュリティ
2. 人間の意図と最終判断
3. ゲームとしての品質と一貫性
4. 再現性と追跡可能性
5. 保守性とAI・ツールの交換可能性
6. 複数タイトルへの再利用性
7. 制作速度と自動化率
8. 費用対効果

速度や自動化のために、品質、権利、保守性、人間の承認を省略してはならない。

---

## 11. Success Criteria

### Studio Foundation

- 新しいAIやツールへ交代しても、役割、判断、作業を引き継げる。
- チャットを変更しても、GitHub上の文書から作業を再開できる。
- タイトル固有情報と共通基盤が分離されている。
- 重要な判断、生成条件、変更履歴を追跡できる。

### Game Production

- 企画から実装、アセット、シナリオ、QA、リリース判断まで一貫した工程を実行できる。
- 共通テンプレートとworkflowを新規タイトルで再利用できる。
- AI生成物が定められたレビューと人間承認を通過している。
- ローカルPCに画像生成用VRAMがなくても、承認されたColabセッション中に制作できる。

### Human Collaboration

- 人間が担当する入力・判断と、AIが担当する実作業が明確である。
- AIだけで解決できない企画判断が、3ラウンド以内に人間へ適切にエスカレーションされる。
- 人間が理解できない仕様、コード、生成物を未確認のまま採用しない。

### Business and Operation

- タイトルごとの制作費、外部サービス費、運用負担を把握できる。
- リリース後の結果を次のタイトルと共通基盤へ反映できる。
- 継続制作に必要な品質、速度、費用、収益性を比較・改善できる。

具体的な数値目標は、実制作で基準値を取得した後、Project Statusまたはゲーム別計画で設定する。根拠のない自動化率や削減率を成功条件として固定しない。

---

## 12. Constraints and Assumptions

- 人間が最終責任者であり、完全無人運用を前提としない。
- 有料サービス、ライセンス、公開、リリースは人間の承認なしに実行しない。
- 有料Google Colabのセッションは人間が開始し、終了後は接続状態に依存しない形で成果物と設定を保存する。
- AIの機能、価格、利用規約、接続方法は変化するため、利用前に確認する。
- 未検証のAI能力を、実行可能な機能として扱わない。
- AI生成物には品質、権利、再現性の確認が必要である。
- 正式情報はGitHubの `main` ブランチへ承認・反映する。

---

## 13. Non-Goals

本プロジェクトは、次を最終目的としない。

- 特定の1タイトルだけに最適化された制作環境
- 人間の創作判断や責任を排除した完全自律開発
- 特定のAIモデルやサービスへ恒久的に依存する構成
- 品質、権利、保守性を犠牲にした自動化率の最大化
- 検証していないAI機能を前提にした制作計画

---

## 14. Related Documents

- `Docs/00_AI_BOOTSTRAP.md`：起動規約と権限境界
- `Docs/02_AI_ROLES.md`：役割、能力要件、担当AI
- `Docs/03_AI_RULES.md`：AIの行動規則
- `Docs/04_PROJECT_STATUS.md`：現在の進捗
- `Docs/06_ARCHITECTURE.md`：技術構成
- `Docs/07_ASSET_PIPELINE.md`：画像・Live2D制作工程
- `Docs/08_SCENARIO_PIPELINE.md`：シナリオ制作工程
- `Docs/09_QA_RELEASE_POLICY.md`：品質・リリース基準
- `Docs/10_REPOSITORY_STRUCTURE.md`：配置・命名規則

---

End of Project Overview.
