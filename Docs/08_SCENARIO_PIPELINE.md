# Scenario Pipeline

Version: 1.0.0  
Last Updated: 2026-08-24  
Status: Active Design / Implementation Pending

---

## 1. Purpose

本書は、ラノベ系文章、キャラクター会話、プロット、分岐、ゲーム実装用シナリオデータを一貫して制作・レビュー・管理する標準工程を定義する。

シナリオを単発の文章生成として扱わず、企画、設定、本文、レビュー、実装、更新まで追跡可能にする。

---

## 2. Core Policy

- シナリオ制作を企画やコード生成の付随作業にしない。
- プロット、本文、レビュー、実装用データを分離する。
- キャラクター設定と世界観をStory Bibleで一元管理する。
- 重要設定と物語方向は人間が承認する。
- ラノベ系の読みやすさ、会話の自然さ、キャラクター差を重視する。
- AIモデルは代表サンプルのブラインド比較で選定する。
- 本文作成者とReviewerを可能な限り別モデル系統にする。
- AIが未承認の設定を本文だけで確定しない。
- 採用本文と生成途中案を区別する。

---

## 3. Roles

| Role | Responsibility |
|---|---|
| Human Creative Owner | テーマ、方向性、重要設定、採用本文の最終承認 |
| Scenario Planner | Story Bible、プロット、分岐、Scene構成 |
| Scenario Writer | ラノベ系本文、会話、地の文 |
| Character Reviewer | 口調、感情、行動、関係性の一貫性 |
| Continuity Reviewer | 時系列、設定、伏線、Scene間の矛盾 |
| Game Integration Editor | ID、分岐、条件、Unity用データへの変換 |
| QA Reviewer | 誤字、表示、分岐到達、データ整合性 |

同一AIが複数Roleを担当する場合も、工程とレビュー会話を分離する。

---

## 4. Required Source Documents

シナリオ開始前に、最低限次を確認する。

- Game Concept
- Target Audience and Rating
- Story Theme
- World Bible
- Character Sheets
- Relationship Map
- Terminology / Naming Rules
- UI Text Constraints
- Scenario Format
- Prohibited Elements
- Release Platform Requirements

未作成の項目はASSUMPTIONではなくPROPOSALとして人間へ確認する。

---

## 5. Story Bible

Story Bibleは、シナリオのSSOTとしてゲーム別に管理する。

最低限の項目：

- World Rules
- Time / Place
- Technology / Magic / Social Rules
- Main Theme
- Tone
- Character Facts
- Character Goals and Conflicts
- Relationship Facts
- Speech Rules
- Known Timeline
- Fixed Events
- Forbidden Contradictions
- Approved Terminology
- Open Questions

本文で新しい恒久設定を採用した場合は、本文だけでなくStory Bibleも更新する。

---

## 6. Production Workflow

### Gate A: Human Direction

人間が目的、テーマ、対象、長さ、表現範囲、必須要素、禁止要素を入力する。

### Stage 1: Concept and Story Goal

- シナリオの役割
- プレイヤーへ与える感情
- 開始状態と終了状態
- ゲーム進行上の目的
- 必須情報
- 選択や分岐の必要性

### Stage 2: Plot

Scenario Plannerが次を作成する。

- Setup
- Inciting Event
- Development
- Turning Point
- Climax
- Resolution
- Character Arc
- Required Game Events
- Branch Points
- Continuity Dependencies

主要な物語方向は人間承認を受ける。

### Stage 3: Scene Outline

各Sceneへ次を定義する。

- Scene ID
- Purpose
- Location / Time
- Characters
- Entry Condition
- Emotional Start / End
- Required Information
- Conflict
- Exit / Next Scene
- Estimated Length

### Stage 4: Draft

Scenario WriterがOutlineに従って本文を作成する。

ラノベ系文章の基本評価軸：

- 冒頭で状況が理解できる。
- 地の文と会話の比率が意図に合う。
- 誰の発言か判別できる。
- キャラクターごとの語彙と文体が異なる。
- 説明を会話だけへ不自然に押し込まない。
- 同じ感情や情報を過度に反復しない。
- 1Scene内の目的と変化が明確である。
- ゲーム表示で読める長さへ分割できる。

### Stage 5: Independent Review

少なくとも次を分けて確認する。

- Character Review
- Continuity Review
- Plot / Pacing Review
- Language / Typo Review
- Platform / Rating Review
- Implementation Review

ReviewerはApprove、Revise、Blockのいずれかと理由を返す。

### Gate B: Human Story Approval

人間が物語方向、キャラクター性、表現、採用本文を判断する。

### Stage 6: Game Data Conversion

承認本文をUnityで扱えるデータへ変換する。

変換時に本文を無断で改稿しない。表示上の分割や制御タグ変更は、原文との対応を保持する。

### Stage 7: In-Game QA

- 文章欠落
- 文字化け
- 話者ID
- 表情・モーション指定
- 分岐条件
- 到達不能Scene
- 無限ループ
- Save / Load
- Localization準備
- 表示速度と改ページ
- 音声や演出との同期

---

## 7. Scenario Data Contract

基本データ例：

```json
{
  "scenario_id": "game01_ch01",
  "scene_id": "game01_ch01_sc001",
  "line_id": "game01_ch01_sc001_0010",
  "speaker_id": "char_a",
  "text": "表示本文",
  "emotion": "neutral",
  "expression_id": "exp_neutral",
  "motion_id": null,
  "background_id": "bg_room_day",
  "choices": [],
  "next_line_id": "game01_ch01_sc001_0020",
  "conditions": [],
  "source_version": "1.0.0"
}
```

実際のschemaはゲームテンプレートで定義し、タイトルごとに無秩序に変更しない。

---

## 8. ID Rules

- IDは一度公開・実装した後に安易に変更しない。
- 表示名と内部IDを分離する。
- 0埋め桁数をタイトル内で統一する。
- Branch、Choice、Flag、Character、Expression、Motionは別Namespaceにする。
- ID変更時は参照箇所とMigrationを確認する。

推奨形式：

```text
<game>_<chapter>_<scene>_<type><number>
```

---

## 9. Model Evaluation

Scenario Writer候補は、同一のStory Bible、Outline、文字数、禁止事項で比較する。

評価表：

- 日本語の自然さ
- ラノベ系の読みやすさ
- キャラクター差
- 会話のテンポ
- 設定遵守
- 長文一貫性
- 修正指示への追従
- 分岐理解
- 出力形式の安定性
- 費用、速度、利用条件

モデル名を見せないブラインド評価を人間が行い、採用理由をモデルレジストリへ記録する。

現行候補はClaude Opus 5、代替候補はGPT-5.6 Solとするが、評価完了前は正式採用としない。

---

## 10. Storage Plan

目標配置：

- Story Bible：`Games/<game-id>/Scenario/Bible/`
- Plot：`Games/<game-id>/Scenario/Plot/`
- Draft：`Games/<game-id>/Scenario/Drafts/`
- Approved Source：`Games/<game-id>/Scenario/Approved/`
- Game Data：`Games/<game-id>/Scenario/Data/`
- Review：`Games/<game-id>/Scenario/Reviews/`
- Shared Template：`Templates/Scenario/`
- Conversion Workflow：`Workflows/Scenario/`

一時出力や不採用案をApprovedへ混在させない。

---

## 11. Versioning

- Story Bible変更は影響範囲を記録する。
- 本文とゲームデータのVersionを対応付ける。
- 承認済み本文を上書きする場合は変更理由を残す。
- 大きな物語変更はDecision Logへ記録する。
- 公開済みシナリオの変更は、Save Data、分岐、Localizationへの影響を確認する。

---

## 12. Quality Gates

| Gate | Required Approval |
|---|---|
| Direction Gate | Human |
| Story Bible Gate | Human + Continuity Reviewer |
| Plot Gate | Human |
| Draft Gate | Character + Continuity Review |
| Approved Text Gate | Human |
| Data Gate | Integration Editor + QA |
| In-Game Gate | QA + Human for final experience |
| Release Gate | Human |

---

## 13. Acceptance Criteria

- Story Bibleと参照Versionが特定できる。
- Sceneの目的、開始、終了、次のSceneが明確である。
- Character、Timeline、Terminologyに矛盾がない。
- Reviewerの指摘が解決または記録されている。
- 人間が本文を承認している。
- 原文とゲームデータを対応付けられる。
- 分岐と条件をテストしている。
- 未承認案とApprovedを区別している。
- Unityで利用できる形式になっている。

---

End of Scenario Pipeline.
