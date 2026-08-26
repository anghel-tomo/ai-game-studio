# AI Playbook

Version: 1.0.0  
Last Updated: 2026-08-24  
Status: Active

---

## 1. Purpose

本書は、AI Game Studioの各Roleが実務で使う手順、成果物、Review、停止条件をまとめた実践ガイドである。

共通ルールは `Docs/03_AI_RULES.md`、実行状態は `Docs/91_AI_EXECUTION_PROTOCOL.md`、個別Task形式は `Docs/93_AI_TASK_PROTOCOL.md` を正とする。

---

## 2. Common Start

すべてのRoleは次から始める。

1. Task IDとGoalを確認する。
2. 99、00、Status、Decision Log、Handoverを確認する。
3. Domain文書と対象Game文書を読む。
4. Input、Output、Scope、Non-Scopeを確認する。
5. Human Approval Pointを確認する。
6. 利用tool、model、費用、外部接続を確認する。
7. 未確定事項をFACT、ASSUMPTION、PROPOSALへ分ける。

---

## 3. Planning Playbook

### Input

- 人間の目的
- 対象Player
- Platform
- 制作・費用・期間の制約
- 既存資産
- Business Goal

### Procedure

1. Main PlannerがBriefを構造化する。
2. 企画案と判断理由を作成する。
3. Reviewer AがPlayer、UX、Creativeを独立評価する。
4. Reviewer Bが実現性、費用、Riskを独立評価する。
5. Main Plannerが変更点、合意点、未合意点を整理する。
6. 最大3ラウンドで合意を試みる。
7. 未合意なら人間へ選択肢を提示する。
8. 結果をDecision Logへ記録する。

### Output

- Concept
- Target
- Core Loop
- USP
- Scope
- Required Assets / Scenario
- Technical Assumptions
- Risks
- Review Records
- Human Decision

### Stop Conditions

- 3ラウンドで未合意
- Targetまたは目的が決まらない
- 費用や権利条件が不明
- 実現性を判断する情報がない

---

## 4. Architecture Playbook

1. RequirementとNon-Functional Requirementを整理する。
2. 現行ArchitectureとDecision Logを読む。
3. 既存構成で実現できるか確認する。
4. Component、責務、Interface、Data Flowを定義する。
5. Failure、Security、Cost、Migration、Rollbackを設計する。
6. Alternativeを比較する。
7. Architect Reviewを行う。
8. 重大変更は人間承認を受ける。
9. ArchitectureとDecision Logを更新する。

Output：

- Diagram
- Component Table
- Data Contract
- Dependencies
- Security / Cost
- Test Plan
- Migration / Rollback

---

## 5. Development Playbook

1. TaskとAcceptance Criteriaを確認する。
2. 対象Code、Test、設定を読む。
3. 最小変更Planを作る。
4. 作業Branchと最新状態を確認する。
5. CodeとTestを変更する。
6. Lint、Unit、Integration、Buildを可能な範囲で実行する。
7. 実行不能なTestは手動確認手順を残す。
8. Independent Code / Architecture Reviewを行う。
9. 差分、Test、Risk、未確認範囲を報告する。

Do not：

- 既存Codeを読まずに全面置換
- 不要な依存追加
- TestしていないBuildを成功扱い
- mainへ直接反映
- SecretsをCommit

---

## 6. Unity Playbook

1. Unity VersionとProject Pathを確認する。
2. Editor、CLI、MCP等の操作経路を確認する。
3. BackupまたはBranchを確認する。
4. Scene、Prefab、Script、Packageの影響を確認する。
5. 小さく編集する。
6. Console Errorを確認する。
7. Play Modeを確認する。
8. WebGLまたは対象Buildを実行する。
9. Screenshot、log、Build結果を保存する。
10. 人間が操作感と見た目を確認する。

Unityへ接続できない場合は、実行したと報告せず、操作手順と確認項目を出力する。

---

## 7. UI/UX Playbook

1. User GoalとScreen Purposeを定義する。
2. Entry、Exit、User Flowを作る。
3. Normal、Selected、Disabled、Loading、Errorを定義する。
4. Wireframeを作る。
5. Visual DesignとAsset Listを作る。
6. Unity実装仕様へ変換する。
7. 解像度、Safe Area、可読性、入力、Localizationを確認する。
8. 実機またはBuildでUX Reviewを行う。
9. 人間が最終Designを承認する。

---

## 8. Character Illustration Playbook

1. 人間のBriefを取得する。
2. Character Sheetと禁止要素を作る。
3. 候補model / LoRA / workflowを同一条件で比較する。
4. 人間がColabセッションを開始する。
5. 承認範囲内でComfyUI Jobを実行する。
6. seed、prompt、model、workflow、入力、出力を記録する。
7. 破綻と同一性を確認し、必要箇所を修正する。
8. Asset Manifestを作る。
9. 人間が採用候補を承認する。
10. Live2DまたはUnity用形式へ渡す。

停止：

- Colab未開始
- 認証・保存先不明
- License未確認
- 費用範囲不明
- Character方針未承認
- Session切断で成果物を保存できない

---

## 9. Live2D Playbook

1. 承認済みCharacter Designを確認する。
2. Part List、重なり、隠れ領域を定義する。
3. segmentation、inpaint、layer化を実行・検証する。
4. Part IDとPSD等の出力を確認する。
5. Parameter Planを作る。
6. 操作をAUTOMATED、AI_ASSISTED、HUMAN_REQUIRED、UNVALIDATEDへ分類する。
7. 実行可能な範囲だけを操作する。
8. 実行不能箇所は人間用手順へ変換する。
9. Cubism上で変形、Parameter、Physicsを確認する。
10. Unity SDK上で表示とPerformanceを確認する。
11. 人間が動きとCharacter性を承認する。

未検証の自動化を成功扱いにしない。

---

## 10. Scenario Playbook

1. 人間のテーマ、目的、禁止要素を確認する。
2. Story BibleとCharacter Sheetを読む。
3. Plotを作成し、人間承認を受ける。
4. Scene Outlineを作る。
5. WriterがDraftを作る。
6. Character、Continuity、Pacing、Languageを独立Reviewする。
7. 人間が本文を承認する。
8. 承認本文をGame Dataへ変換する。
9. 分岐、ID、表示、演出指定をTestする。
10. Approved SourceとGame DataのVersionを対応付ける。

---

## 11. QA Playbook

1. 仕様、Acceptance Criteria、対象Versionを確認する。
2. RiskとSeverity基準を確認する。
3. Test ScopeとUntestedを定義する。
4. Static、Unit、Integration、Build、Experienceを実行する。
5. Evidenceを保存する。
6. FindingへSeverityと再現手順を付ける。
7. 修正後に回帰Testする。
8. Independent Reviewerが判定する。
9. S0 / S1がある場合はReleaseをBlockする。
10. Human Release Approvalへ結果を渡す。

---

## 12. Research Playbook

1. 調査質問と意思決定への影響を定義する。
2. 変化する情報か判断する。
3. 公式・一次情報を優先して検索する。
4. 実際の根拠ページを確認する。
5. 更新日、Version、Region、Planを確認する。
6. 事実と推論を分ける。
7. 複数案の利点、欠点、費用、Riskを比較する。
8. URLと確認日を残す。
9. 決定は人間または定められた合議へ渡す。

---

## 13. Project Management Playbook

1. GoalをDeliverableへ分解する。
2. Task、依存関係、担当、Review、承認点を定義する。
3. BlockerとCritical Pathを確認する。
4. StatusをFACTで更新する。
5. In Progressを必要以上に増やさない。
6. 変更要求が入った場合はScope、Cost、Scheduleへの影響を出す。
7. 完了時にEvidenceと残課題を確認する。
8. Status、Handover、Contextを更新する。

---

## 14. Documentation Playbook

1. 文書のResponsibilityを確認する。
2. 既存文書とDecision Logを読む。
3. 重複情報を責任文書へ集約する。
4. 変更理由と影響先を確認する。
5. VersionとLast Updatedを更新する。
6. File名、番号、Linkを検査する。
7. 目標と実装済みを区別する。
8. 旧文書は削除承認までDeprecated化する。
9. GitHub上の実Fileを再取得して確認する。
10. mainへのマージ前にIndependent Reviewを行う。

---

## 15. Session End

すべてのRoleは終了前に次を確認する。

- Deliverable
- Test / Review
- Decisions
- Status
- Project Memory
- Session Handover
- AI Context
- Human Approval Pending
- Restart Point

---

End of AI Playbook.
