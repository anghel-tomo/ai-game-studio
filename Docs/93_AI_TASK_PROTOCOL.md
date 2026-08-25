# AI Task Protocol

Version: 1.1.0  
Last Updated: 2026-08-25  
Status: Active

---

## 1. Purpose

本書は、AIOSが個別タスクを受付、実行、検証、完了、引継ぎするためのTask Packet、状態、Risk、成果物、完了条件を定義する。

---

## 2. Task Identity

すべての管理対象Taskは一意なTask IDを持つ。

推奨形式：

```text
<domain>[-<subdomain>]-<number>
```

`subdomain` はTask群を分ける必要がある場合だけ使用する。

例：

- `DOCS-001`
- `DOCS-FOUNDATION-001`
- `PLAN-001`
- `UNITY-001`
- `ASSET-001`
- `LIVE2D-001`
- `SCENARIO-001`
- `QA-001`
- `RELEASE-001`

一度使用したIDを別Taskへ再利用しない。

---

## 3. Task Packet

```yaml
task_id:
title:
status: RECEIVED
goal:
deliverables: []
scope: []
non_scope: []
inputs: []
related_docs: []
dependencies: []
assigned_roles: []
reviewers: []
risk: low
tools: []
external_actions: []
cost:
  class: none
  human_approval: false
human_approval_points: []
acceptance_criteria: []
tests: []
rollback:
branch:
base_commit:
output_paths: []
decisions: []
blockers: []
created_at:
updated_at:
```

Task PacketはIssue、Markdown、YAML等で管理できるが、同じTaskで複数の正本を作らない。

---

## 4. Required Fields

### Goal

「何をするか」ではなく、「完了後に何が実現しているか」を記載する。

Bad：

- Unityを修正する。

Good：

- WebGL BuildでMain MenuからGame Sceneへ遷移でき、Console Errorがない。

### Deliverables

確認可能なFile、Build、Report、Decision、Assetを指定する。

### Scope / Non-Scope

Taskに含むものと含まないものを明記し、途中の無制限な拡張を防ぐ。

### Acceptance Criteria

第三者がPass / Failを判定できる文にする。

### Human Approval Points

承認が必要になる時点と対象を記載する。

---

## 5. Task States

本節をAIOS全体の正規State定義とする。`Docs/91_AI_EXECUTION_PROTOCOL.md`、Task Packet、Execution Logは本節のState名を使用する。

| State | Entry Condition | Exit Condition |
|---|---|---|
| RECEIVED | 依頼受領 | GoalとDeliverableを抽出 |
| NEEDS_CLARIFICATION | 結果が大きく変わる不足情報 | 人間回答 |
| READY | Scope、Role、Riskが確定 | 実行開始 |
| PLANNING | Plan作成中 | Plan確定 |
| APPROVAL_WAIT | 人間承認が必要 | 明示承認 |
| IN_PROGRESS | 実行中 | Deliverable作成 |
| REVIEW | Test / Review中 | ApproveまたはRevise |
| REVISION | 指摘修正中 | 再Review |
| BLOCKED | 外部要因で停止 | 解決またはCancel |
| COMPLETED | 完了条件を満たす | Handover済み |
| CANCELLED | 中止決定 | 状態と影響を記録 |

---

## 6. Risk Classification

### Low

- Read-only確認
- 文言修正
- Draft作成
- 復旧容易な非破壊変更

### Medium

- 新規File
- 通常Code変更
- workflow変更
- AI生成Asset候補

### High

- Architecture変更
- 新規依存
- 外部Write
- 有料処理
- 大規模Asset生成
- Migration

### Critical

- Secrets / Permission
- 削除
- History Rewrite
- Public Deploy
- Store Release
- main Merge
- Data Lossの可能性

High以上はPlanと人間承認点を必須とする。Criticalは明示承認まで実行しない。

---

## 7. Task Decomposition

Taskは次を満たす大きさへ分ける。

- 1つのGoal
- 明確なDeliverable
- 独立したAcceptance Criteria
- 1つの主担当Role
- Review可能
- Block時に他Taskへの影響を説明可能
- 1回のCommitまたは少数Commitへ対応可能

分割しすぎてContext取得Costが成果物より大きくならないようにする。

---

## 8. Dependency Rules

- DependencyはTask IDまたは特定成果物で指定する。
- 「前のTask」など曖昧な表現を使わない。
- 未完了Dependencyがある場合、先行可能な作業だけを分離する。
- 仮成果物へ依存する場合はVersionとStatusを記載する。
- Circular Dependencyを発見した場合はArchitectureまたはPlanを見直す。

---

## 9. Execution Log

Task中は重要な状態変化だけを記録する。

```text
Timestamp:
State:
Action:
Result:
Evidence:
Next:
```

秘密情報、不要な内部思考、長いtool出力をそのまま保存しない。

---

## 10. Change Control

Task開始後に追加指示が入った場合：

1. 元のGoalと両立するか確認する。
2. Scope、Cost、Schedule、Riskへの影響を確認する。
3. 小さな追加ならTask Packetを更新する。
4. Goalが変わる場合は別Taskへ分ける。
5. Human Approval Pointが増える場合は停止する。
6. 変更理由を記録する。

---

## 11. Retry Policy

- 同じ操作を無制限に繰り返さない。
- 1回目の失敗で原因と入力を確認する。
- 2回目も同じ原因で失敗した場合は方法を変える。
- 費用、Data、Security Riskがある場合は自動再試行しない。
- External Serviceの一時障害は、再試行条件と上限を定義する。
- Blocked時は安全なRestart Pointを残す。

---

## 12. Review Packet

```yaml
task_id:
reviewer:
review_scope:
method:
findings:
  - id:
    severity:
    location:
    description:
    required_change:
untested: []
decision: APPROVE
reviewed_at:
```

Reviewerは作成者と異なるRoleまたは独立Sessionを使用する。

---

## 13. Completion Checklist

- [ ] Goal達成
- [ ] Deliverables存在
- [ ] Scope内で完了
- [ ] Acceptance Criteriaを確認
- [ ] Test実施
- [ ] Independent Review実施
- [ ] Findings解決または記録
- [ ] Human Approval境界を遵守
- [ ] Decision Log更新
- [ ] Project Status更新
- [ ] Project Memory更新の要否確認
- [ ] Session Handover更新
- [ ] AI Context更新
- [ ] Branch / Commit / Fileを報告
- [ ] 未確認範囲と次Actionを報告

必要項目が未完了の場合はCOMPLETEDではなくBLOCKED、REVIEW、APPROVAL_WAITのいずれかとする。

---

## 14. Task Result Format

```markdown
## Result

- Task ID:
- Status:
- Outcome:
- Changed:
- Tests:
- Review:
- Human Approval:
- Known Issues:
- Not Done:
- Commit / PR:
- Next Action:
```

Outcomeを先に記載し、toolの操作説明だけで終わらせない。

---

## 15. Domain Requirements

### Planning Task

- 3者合議記録
- Round数
- Human Escalationの要否

### Development Task

- Branch
- Code差分
- Test / Build
- Rollback

### Asset Task

- Human Brief
- Model / Workflow / Seed
- Asset Manifest
- License
- Human Art Approval

### Live2D Task

- Part List
- Parameter Plan
- Automation Status
- Cubism / Unity QA
- Human Approval

### Scenario Task

- Story Bible Version
- Plot / Draft / Approved
- Reviewer
- Data Conversion
- Branch Test

### Release Task

- Version / Commit
- QA Evidence
- Rights / Security
- Known Issues
- Rollback
- Human Release Approval

---

End of AI Task Protocol.
