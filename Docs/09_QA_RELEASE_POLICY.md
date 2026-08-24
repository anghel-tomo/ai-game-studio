# QA and Release Policy

Version: 1.0.0  
Last Updated: 2026-08-24  
Status: Active Design / Implementation Pending

---

## 1. Purpose

本書は、文書、コード、ゲーム、UI、画像、Live2D、シナリオ、外部サービス設定を検証し、Release Candidateから公開まで進めるための品質基準を定義する。

AIによる検証は人間の最終リリース判断を代替しない。

---

## 2. Quality Principles

- 仕様に適合していることを、生成者の自己評価だけで判断しない。
- テストした範囲と未テスト範囲を分離する。
- 実行結果の証拠を残す。
- 重大な問題を既知のままReleaseしない。
- 権利、セキュリティ、データ損失、課金事故を機能不具合より軽く扱わない。
- WebGLで早期検証し、対象プラットフォーム固有確認を省略しない。
- ReleaseはVersion、Commit、成果物、設定を再現可能にする。
- 公開とデプロイは人間承認後に行う。

---

## 3. Artifact Status

- `DRAFT`：作成中
- `READY_FOR_REVIEW`：作成者確認済み
- `CHANGES_REQUIRED`：修正必要
- `APPROVED`：担当Review通過
- `RELEASE_CANDIDATE`：Release Gate確認待ち
- `RELEASED`：人間承認後に公開済み
- `BLOCKED`：重大問題または承認待ち
- `DEPRECATED`：新規利用停止
- `SUPERSEDED`：後継へ置換済み

---

## 4. Defect Severity

| Severity | Definition | Release Rule |
|---|---|---|
| S0 Critical | データ損失、権利侵害、秘密漏えい、不正課金、起動不能、重大Security | Release禁止 |
| S1 High | 主要進行不能、主要機能破綻、重大な表示・シナリオ欠落 | 原則Release禁止 |
| S2 Medium | 回避可能な不具合、限定条件の誤動作、品質低下 | 人間承認と対応計画が必要 |
| S3 Low | 軽微な表示、誤字、改善要望 | 記録のうえ人間判断 |
| S4 Observation | 将来改善、未確定懸念 | Backlogへ記録 |

Severityを下げる場合は、理由と影響範囲を記録する。

---

## 5. Test Levels

### L1: Static Validation

- Markdown、JSON、YAML、CSV等の構文
- 命名、ID、参照先
- 未使用ファイル、重複、リンク切れ
- Secretsや個人情報の混入
- ライセンス情報

### L2: Unit / Component Test

- 個別ロジック
- Unity Component
- データ変換
- Scenario Parser
- Asset Manifest Validator
- Editor Tool

### L3: Integration Test

- UnityとFirebase
- UnityとLive2D SDK
- Scenario DataとUI
- Build Pipeline
- ComfyUI workflowと保存先
- AIOS Taskと成果物

### L4: Build Test

- Unity Editor実行
- WebGL Build
- 対象プラットフォームBuild
- CI Build
- Development / Release設定差

### L5: Experience Test

- ゲーム進行
- UI・UX
- 入力
- 表示解像度
- パフォーマンス
- Live2D品質
- シナリオテンポ
- Save / Load
- Error / Offline状態

### L6: Release Validation

- VersionとCommit
- Release Notes
- 権利・ライセンス
- Privacy / Data Handling
- Secrets
- 配信設定
- Rollback
- 人間承認

---

## 6. Domain QA

### Documentation

- 1文書1責務
- VersionとLast Updated
- ファイル名と番号
- 文書間リンク
- Decision、Status、Context、Handoverの整合性
- 実装済みと目標の区別
- 旧文書のDeprecatedまたはSuperseded表示

### Code and Architecture

- 仕様適合
- Architectureとの整合
- 依存関係とライセンス
- Error処理
- Test
- Performance
- Security
- Rollback

### UI/UX

- User Flow
- 通常、選択、無効、Loading、Error状態
- Safe Areaと解像度
- 可読性
- 入力方法
- Localization
- Accessibility
- Unity実装との一致

### Character and Assets

- Character同一性
- 破綻、透過、色、解像度
- 生成条件の再現性
- Rights / License
- Human Art Approval
- Manifestと出力対応

### Live2D

- Part境界
- 変形
- Parameter範囲
- Physics
- Motion / Expression
- Unity SDK表示
- 対象端末Performance
- Human Motion Approval

### Scenario

- Character Voice
- Continuity
- Timeline
- Terminology
- Branch Reachability
- Display / Encoding
- Approved Textとの一致
- Rating / Platform Requirements

---

## 7. Review Separation

重要成果物は次の順序を基本とする。

```text
Author Self-Check
  → Independent AI Review
  → Architecture / Domain Review
  → Automated or Manual Test
  → Human Approval
```

- 実装担当と最終Reviewerを可能な限り別モデル系統にする。
- 同一モデルの場合は独立セッションに分ける。
- Reviewerは、対象、確認方法、Findings、判定、未確認項目を出力する。
- 「問題なし」だけのReviewを有効としない。

---

## 8. Evidence Requirements

Test結果には最低限次を残す。

- Task ID
- Commit / Build Version
- Environment
- Test Date
- Tester / AI Role
- Test Scope
- Input / Preconditions
- Expected Result
- Actual Result
- Evidence
- Defects
- Untested Areas
- Final Status

証拠例：

- Test log
- Build log
- Screenshot
- Screen recording
- Generated report
- Hash
- Pull Request review

秘密情報はEvidenceへ含めない。

---

## 9. Release Gates

### Gate 1: Scope Freeze

- Release対象と非対象を確定
- 主要仕様変更を停止
- Known Issuesを整理

### Gate 2: Build Candidate

- Versionを設定
- 対象Commitを固定
- 再現可能なBuildを作成
- Build logを保存

### Gate 3: Technical QA

- S0 / S1が0件
- 必須Testが完了
- SecurityとSecretsを確認
- 未確認範囲を明示

### Gate 4: Content and Asset QA

- シナリオ承認
- UI・画像・Live2D承認
- 権利とライセンス確認
- 配信素材確認

### Gate 5: Human Release Approval

人間が、品質、費用、権利、公開範囲、Known Issues、Rollbackを確認する。

### Gate 6: Publish

承認された操作だけを実行し、公開後の確認を行う。

---

## 10. Release Checklist

- [ ] Release Scope確定
- [ ] Version / Commit確定
- [ ] Build成功
- [ ] 必須Test成功
- [ ] S0 / S1なし
- [ ] Known Issues記録
- [ ] Secrets混入なし
- [ ] Rights / License確認
- [ ] Privacy / Data Handling確認
- [ ] UI / Asset / Live2D承認
- [ ] Scenario承認
- [ ] Store / Platform設定確認
- [ ] Release Notes作成
- [ ] Backup / Rollback確認
- [ ] Human Approval記録
- [ ] Publish後確認
- [ ] Status / Handover更新

チェックを推測で完了にしない。

---

## 11. Rollback Policy

Release前に次を用意する。

- 直前の安定Version
- 対象Commit / Tag
- Backend変更の戻し方
- Data MigrationのBackup
- 配信停止または旧Versionへ戻す手順
- 連絡・判断担当
- Rollback実行条件

データ消失や課金事故の可能性がある場合、AIが単独でRollbackを実行しない。

---

## 12. Hotfix

1. 問題を再現しSeverityを判定する。
2. Hotfix範囲を最小化する。
3. 対象BranchとVersionを確認する。
4. 修正と回帰Testを行う。
5. Independent Reviewを行う。
6. 人間が公開を承認する。
7. Decision LogまたはRelease Notesへ記録する。
8. 通常Branchへ変更を戻し忘れない。

---

## 13. Release Completion Criteria

- 公開対象と実際の成果物が一致する。
- Human Approvalが記録されている。
- 公開後の起動・主要導線を確認している。
- Version、Commit、Build、設定を追跡できる。
- Known IssuesとRollbackが参照できる。
- Status、Memory、Handover、Contextが更新されている。

---

End of QA and Release Policy.
