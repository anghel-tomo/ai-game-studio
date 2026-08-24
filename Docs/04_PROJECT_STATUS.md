# Project Status

Version: 1.0.1  
Last Updated: 2026-08-24  
Status: Active

---

## 1. Current Summary

| Item | Current State |
|---|---|
| Project Stage | Stage 1: Governance Foundation |
| Overall Status | Ready for Independent Review |
| Repository | `anghel-tomo/ai-game-studio` |
| Default Branch | `main` |
| Documentation Branch | `codex/aios-docs-revision` |
| Current Focus | Independent Reviewと人間の最終確認 |
| Human Decision Required | mainへのマージ、旧文書の削除 |
| Next Major Stage | Stage 2: Reusable Production Foundation |

作業ブランチ上の内容は、mainへマージされるまで正式決定ではない。

---

## 2. Completed

- GitHubリポジトリを公開し、SSOTとして利用できる状態にした。
- 基本フォルダ `Docs/`、`Games/`、`Templates/`、`Tools/`、`Workflows/`、`Scripts/`、`Assets/` を作成した。
- 最終構成のCore Documents `00`～`12` を作成した。
- Operational Documents `91`～`93` と `99_AI_CONTEXT.md` を作成した。
- READMEを新文書構成とApache License 2.0へ整合させた。
- 旧番号文書3件を削除せずDeprecated化した。
- 企画の3者合議、最大3ラウンド、人間エスカレーションを文書化した。
- Stable Diffusion + ComfyUI + Human-Started Colabを文書化した。
- AIによるLive2Dパーツ・パラメーター作成の目標と未検証範囲を文書化した。
- ラノベ系Scenario Pipelineを文書化した。
- GitHub上から全対象Fileを再取得し、必須17文書、Metadata、README Link、主要方針を検査した。
- README内の相対Link 26件にBroken Linkがないことを確認した。

---

## 3. In Progress

- Independent Reviewer AIの選定
- Independent Reviewer AIによる文書全体Review
- 人間による最終確認
- Review Findingがある場合の修正
- mainへのマージ判断

- Core Documents `02`～`06` の作成
- Production Documents `07`～`12` の作成
- Operational Documents `91`～`93`、`99` の作成
- 旧番号文書と新番号文書の競合解消
- READMEの文書一覧、ライセンス表記、現在状態の整合性確認
- 文書間リンク、Version、用語、承認境界の統一

---

## 4. Not Started

- モデルレジストリの実ファイル作成と代表タスク評価
- Unity 6テンプレートの構築
- Unity CLI / MCP / Computer Use操作の実機検証
- Firebaseプロジェクトと安全な秘密情報管理の構築
- WebGL自動ビルド・デプロイ
- ComfyUI用Colabノートブックとworkflowの実装
- Stable Diffusionモデル、LoRA、ControlNet等の比較評価
- Live2Dパーツ制作・パラメーター作成の自動化検証
- ラノベ系シナリオモデルのブラインド比較
- QAテンプレートとリリースチェックリストの実装
- 最初の検証ゲーム企画

Not Startedの項目を実装済みとして扱ってはならない。

---

## 5. Confirmed Decisions

詳細は `Docs/05_DECISION_LOG.md` を正とする。

- GitHubのmainを承認済み情報のSSOTとする。
- 人間を最終判断者とする。
- AIは役割と能力要件で選定し、モデル名へ恒久固定しない。
- 企画は3者合議、最大3ラウンドとする。
- キャラクターイラストの主系統はStable Diffusion + ComfyUIとする。
- 有料Colabは人間がセッションを開始する。
- GPT-Image-2とNano Banana Proを、本番キャラクターイラストの主系統にしない。
- Live2D自動化は目標であり、現時点で検証済みとは扱わない。
- シナリオ制作を独立したPipelineとして管理する。
- mainへのマージと破壊的操作は人間承認を必要とする。

---

## 6. Risks

| Risk | Impact | Current Response |
|---|---|---|
| Live2D自動化能力が未検証 | 制作工程に人間操作が残る可能性 | 工程単位で検証し、Human Fallbackを残す |
| ローカルPCに画像生成用VRAMがない | ローカル生成不可 | 有料Colabを人間が開始し、成果物を永続保存 |
| Colabセッション切断 | 作業・成果物の消失 | checkpoint、workflow、ログを外部保存 |
| AIモデルと規約の変化 | 役割割当の陳腐化 | モデルレジストリとLast Verifiedを管理 |
| Previewモデルへの依存 | 突然の変更・停止 | Stableまたは別ProviderのFallbackを用意 |
| 旧番号文書の残存 | AIが誤った文書を読む | 新文書を作成し、旧文書は明示的にDeprecated化 |
| フォルダがプレースホルダーのみ | 実装済みと誤認 | StatusでNot Startedを明示 |
| READMEとLICENSEの表記差 | 公開時の誤解 | LICENSEを正としてREADMEを修正予定 |
| 外部サービス費の増加 | 継続運用に影響 | 人間承認と費用記録を必須化 |

---

## 7. Blockers

現時点で、文書作成を止めるBlockerはない。

実装段階では次がBlockerとなり得る。

- Colab、Unity、Firebase、Live2D Cubism等への未接続
- 利用するモデル、チェックポイント、LoRAのライセンス未確認
- 有料サービス開始の人間承認未取得
- Unity操作環境または必要プラグインの不足
- Live2Dパラメーター作成を自動化する手段の未検証

---

## 8. Immediate Next Actions

1. Independent Reviewer AIで文書全体をReviewする。
2. FindingをSeverity別に整理する。
3. 必要な修正を作業Branchへ反映する。
4. 人間が最終差分を確認する。
5. 人間が旧文書削除の要否とmainへのマージを判断する。
6. 承認後、Stage 2の最初の実装Taskを決定する。

---

## 9. Status Update Rules

- 作業開始時にCurrent Focusを確認する。
- 進捗、Blocker、次の作業が変わった場合に更新する。
- セッション終了時に実行済みと未実行を分離する。
- 完了した項目をNot Startedへ残さない。
- 推測や予定をCompletedへ記載しない。
- 詳細な履歴はDecision Log、長期知識はProject Memoryへ移す。

---

End of Project Status.
