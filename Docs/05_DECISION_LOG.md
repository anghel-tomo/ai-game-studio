# Decision Log

Version: 1.1.0  
Last Updated: 2026-08-25  
Status: Active

---

## 1. Purpose

本書は、AI Game Studioの重要判断、理由、代替案、影響、置換関係を記録する。

結果だけでなく「なぜその案を採用したか」を残し、別のAIや将来のセッションが同じ議論を繰り返さないようにする。

---

## 2. Status Definitions

- `PROPOSED`：提案中
- `ACCEPTED`：承認済み
- `REJECTED`：不採用
- `SUPERSEDED`：新しい決定に置換済み
- `DEPRECATED`：移行期間後に使用停止予定

---

## 3. Decision Records

### D-001: GitHub mainをSSOTとする

- Date: 2026-08-24 reconfirmed
- Status: ACCEPTED
- Decision: 人間が承認しmainへ反映した文書、コード、履歴を正式情報とする。
- Reason: チャットやAIの記憶に依存せず、複数AIと複数セッションで情報を共有するため。
- Consequence: 作業ブランチは提案状態であり、mainへのマージには人間承認が必要。

### D-002: 最終文書構成を00～12、91～93、99とする

- Date: 2026-08-24
- Status: ACCEPTED
- Decision: Core Documentsを00～12、Operational Documentsを91～93、Current Contextを99で管理する。
- Reason: 文書ごとの責務を分離し、読込対象と更新先を明確にするため。
- Consequence: 旧番号の `02_AI_RULES.md`、`03_PROJECT_STATUS.md`、`04_SESSION_HANDOVER.md` は移行対象となる。

### D-003: AIを役割と能力要件で選定する

- Date: 2026-08-24
- Status: ACCEPTED
- Decision: モデル名を恒久的な役割名にせず、Role、Capability、Status、Fallbackをモデルレジストリで管理する。
- Reason: モデルとサービスの更新、価格、規約、可用性の変化へ対応するため。
- Rejected Alternative: 特定モデルを全タスクの固定担当とする。
- Consequence: Primary変更時は代表タスク評価、人間の明示承認、Decision Log更新が必要。

### D-004: 企画は3者合議とする

- Date: 2026-08-24
- Status: ACCEPTED
- Decision: Main Planner、Reviewer A、Reviewer Bが独立して検討し、3者が同一案を承認した場合に合意とする。
- Reason: 企画の自己正当化と単一視点への偏りを減らすため。
- Consequence: Reviewer Aはプレイヤー・創作視点、Reviewer Bは実現性・リスク視点を担当する。

### D-005: 企画合議は最大3ラウンドとする

- Date: 2026-08-24
- Status: ACCEPTED
- Decision: 3ラウンド終了時に未合意なら、多数決や強制採択をせず人間へ判断を求める。
- Reason: AI同士の無限議論を防ぎ、人間の最終決定権を維持するため。
- Consequence: エスカレーション時は選択肢、利点、欠点、未合意点、推奨案を提示する。

### D-006: キャラクターイラストの主系統をStable Diffusion + ComfyUIとする

- Date: 2026-08-24
- Status: ACCEPTED
- Decision: 本番キャラクターイラストはStable DiffusionをComfyUIから利用する。
- Reason: キャラクター品質、再現性、workflow制御、LoRA等の拡張性を重視するため。
- Consequence: workflow、model、LoRA、seed、prompt、設定を保存する。

### D-007: 有料Colabは人間がセッションを開始する

- Date: 2026-08-24
- Status: ACCEPTED
- Decision: ローカルPCに画像生成用VRAMがないため、有料Google ColabのVRAMを使用する。セッション開始は人間が行い、稼働中はComfyUIとAIOSから操作する。
- Reason: 費用と認証を人間が管理しながら、AIによる制作操作を可能にするため。
- Consequence: AIは無断開始・延長せず、切断前に成果物と設定を永続保存する。

### D-008: GPT-Image-2とNano Banana Proを本番キャラクターの主系統にしない

- Date: 2026-08-24
- Status: ACCEPTED
- Decision: GPT-Image-2とNano Banana Proは、本プロジェクトで必要とする最終キャラクターイラスト品質に不足があるため、主系統へ採用しない。
- Reason: 人間による品質評価。
- Consequence: 将来再評価する場合も、Stable Diffusion系workflowと同条件の代表サンプルで比較する。

### D-009: Live2Dの目標範囲をパーツ・パラメーター作成までとする

- Date: 2026-08-24
- Status: ACCEPTED
- Decision: 人間が指示・入力と最終確認を行い、AIがパーツ制作とパラメーター設計・作成まで担当することを目標とする。
- Reason: 人間の制作負担を減らしつつ、最終品質判断を残すため。
- Supersedes: 人間がLive2Dモデリング全体を担当する旧方針。
- Consequence: 現在は未検証のため、工程別に自動化可能範囲とHuman Fallbackを確認する。

### D-010: シナリオ制作を独立Pipelineとする

- Date: 2026-08-24
- Status: ACCEPTED
- Decision: ラノベ系文章、会話、プロット、分岐、推敲、実装用データ変換を独立した制作工程として管理する。
- Reason: シナリオ品質と設定整合性を、企画やコード生成の付随作業にしないため。
- Consequence: `Docs/08_SCENARIO_PIPELINE.md`で工程と品質基準を定義する。

### D-011: 技術基盤はUnity 6、Firebase、WebGL-firstを基本とする

- Date: 2026-08-24 reconfirmed
- Status: ACCEPTED
- Decision: Unity 6をゲーム基盤、Firebaseをバックエンド基本候補、WebGLを早期検証手段とする。
- Reason: 複数プラットフォーム展開、個人開発での運用性、早期確認を両立するため。
- Consequence: 詳細と変更はArchitectureへ記録し、代替技術への置換は人間承認を必要とする。

### D-012: 破壊的操作とmainへのマージは人間承認を必要とする

- Date: 2026-08-24
- Status: ACCEPTED
- Decision: 削除、履歴書換え、復旧困難な操作、mainへのマージはAIが単独で実行しない。
- Reason: SSOTの損失と意図しない正式反映を防ぐため。
- Consequence: 文書移行中の旧ファイルは、承認なしに削除せずDeprecated化する。

### D-013: Semantic Versioningを文書へ適用する

- Date: 2026-08-24
- Status: ACCEPTED
- Decision: Majorを互換性のない規約変更、Minorを機能・責務追加、Patchを明確化・誤記修正に使用する。
- Reason: AIが変更の重要度を判断しやすくするため。
- Consequence: 内容変更時にVersionとLast Updatedを更新する。

### D-014: 独立Review Findingの採否と修正方針

- Date: 2026-08-25
- Status: PROPOSED
- Decision: 3回のClaude Free ReviewをFinding ID単位で照合し、実在する矛盾・欠落を修正する。重複、依頼文の誤記、Repositoryに存在しない前提に基づく指摘は理由付きで不採用とする。
- Accepted Findings: R1-001～R1-011、R2-001～R2-010、R2-012、R3-005、R3-007。R3-001はStatus / Handover更新の時点差として是正するが、「Review→Fix運用が機能していない」という評価は採用しない。
- Rejected Findings:
  - R2-011 / H-4：人間の要件は「Main Planner 1名 + Reviewer 2名 = 合計3者」であり、全文書の3者合議と一致する。
  - R3-006：Review報告書はClaudeへ添付した外部Fileであり、Repository Rootへ格納されているという前提が事実と異なる。
  - R3-008：`99_DOCUMENT_MAP.md` はReview依頼文側の誤記であり、Repositoryの正規Fileは `99_AI_CONTEXT.md` である。
- Reason: 独立Reviewを尊重しつつ、Reviewerの推測や時点差をSSOTへ誤反映しないため。
- Consequence: 修正後にFocused Re-reviewを行い、人間が本Decisionと差分を承認するまでmainへマージしない。

### D-015: Pilot期間のOrchestratorとRelease Coordinator

- Date: 2026-08-25
- Status: PROPOSED
- Decision: AIOS OrchestratorがActiveとして検証されるまで、Human Project Ownerが暫定Orchestratorとなり、手動実行またはProject Managerへ明示委任する。Release Coordinatorの実行主体はProject Managerとし、検証済みAIOS Release WorkflowはAlternativeとする。
- Reason: 未検証の自動Orchestratorを前提にせず、Task Router、Review、Release準備の責任主体を明確にするため。
- Consequence: Task Packetへ実行主体と委任範囲を記録する。自動化への切替はCapability Validationと人間承認後に行う。

---

## 4. New Decision Template

新しい判断は、次の形式で追記する。

```markdown
### D-XXX: Decision Title

- Date: YYYY-MM-DD
- Status: PROPOSED | ACCEPTED | REJECTED | SUPERSEDED | DEPRECATED
- Decision:
- Reason:
- Alternatives:
- Consequence:
- Human Approval:
- Related Files:
- Supersedes:
```

---

## 5. Update Rules

- 既存記録を削除せず、StatusとSupersedesで関係を残す。
- AIが単独でACCEPTEDへ変更できるのは、既存規則で承認権限が与えられた範囲だけとする。
- 人間判断を伴う決定は、Human Approvalを記録する。
- 変更によって影響を受ける文書を同じタスク内で更新する。
- 番号は再利用しない。
- 詳細な議論ログを貼り付けず、判断に必要な要点を残す。

---

End of Decision Log.
