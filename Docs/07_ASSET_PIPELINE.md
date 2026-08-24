# Asset Pipeline

Version: 1.0.0  
Last Updated: 2026-08-24  
Status: Active Design / Implementation Pending

---

## 1. Purpose

本書は、UI、キャラクターイラスト、画像パーツ、Live2Dデータを、再現可能かつレビュー可能な形で制作する標準工程を定義する。

目標工程を示す文書であり、すべての自動化を検証済みとするものではない。実装状態は `Docs/04_PROJECT_STATUS.md` を正とする。

---

## 2. Core Policy

- 本番キャラクターイラストはStable Diffusion + ComfyUIを主系統とする。
- ローカルPCに画像生成用VRAMがないため、有料Google Colabを使用する。
- Colabセッションは人間が開始する。
- 稼働中のセッションをComfyUIとAIOSから操作する。
- GPT-Image-2とNano Banana Proは、本番キャラクターイラストの主系統にしない。
- workflow、model、LoRA、seed、prompt、入力、主要設定を保存する。
- 人間が指示・入力と最終採用判断を行う。
- 権利、ライセンス、品質が確認できない資産を本番採用しない。
- セッション終了後も再開できる状態で成果物を保存する。

---

## 3. Asset Categories

| Category | Examples | Final Owner |
|---|---|---|
| Character Master | 立ち絵、基準表情、衣装、色指定 | Human Approval |
| Character Variations | 表情、ポーズ、衣装差分 | Character Illustrator |
| UI/UX | 画面、ボタン、アイコン、背景、状態差分 | UI/UX Designer |
| Live2D Source | パーツ分け画像、レイヤー、マスク | Live2D Pipeline Agent |
| Live2D Model | パラメーター、物理演算、モーション、書出し | Live2D Pipeline Agent + Human QA |
| Shared Assets | 共通エフェクト、汎用背景、テンプレート | Asset Manager |
| References | ムードボード、構図、色、資料 | Human / Researcher |

参考画像と本番採用画像を同じ場所・同じStatusで管理しない。

---

## 4. Character Illustration Workflow

### Gate A: Human Brief

人間が最低限次を入力する。

- ゲームとキャラクターの目的
- キャラクター設定
- 年齢表現、体格、服装、髪、色
- 世界観と画風
- 必要な構図、表情、差分
- 禁止要素
- 利用範囲と品質基準
- Live2D利用の有無

不足情報をAIが重要設定として補完する場合は、PROPOSALとして人間へ確認する。

### Stage 1: Character Specification

Character Illustratorは、入力を構造化したCharacter Sheetを作成する。

- Character ID
- Visual Keywords
- Negative Requirements
- Color Palette
- Costume Definition
- Proportion Rules
- Face / Hair Landmarks
- Expression Set
- Required Variations
- Live2D Part Requirements
- Approval Status

### Stage 2: Workflow Selection

利用するStable Diffusion系model、VAE、LoRA、ControlNet等を代表サンプルで比較する。

選定はモデルの人気や説明文だけで決めず、同じBriefと評価表で比較する。

評価軸：

- 顔と身体の品質
- キャラクター同一性
- 衣装・小物の再現
- 指定構図への追従
- 差分制作の安定性
- Live2Dパーツ化のしやすさ
- ライセンス
- VRAM、時間、費用
- 再現性

### Gate B: Colab Session Start

人間が有料Google Colabのセッションを開始し、利用可能なGPUと作業範囲を確認する。

AIは開始済みと確認できるまでGPU処理を始めない。

### Stage 3: ComfyUI Execution

AIOSまたはCharacter Illustratorが、承認済みworkflowをComfyUIで実行する。

記録対象：

- Job ID
- Colab Session IDまたは開始時刻
- ComfyUI Version
- Workflow File and Version
- Checkpoint / VAE / LoRA
- ControlNet等の補助model
- Seed
- Positive / Negative Prompt
- Resolution
- Sampler / Scheduler / Steps / CFG
- Input Image / Mask
- Output File
- Duration / Retry Count

### Stage 4: Selection and Repair

候補を比較し、採用候補へ次を行う。

- 顔、手、衣装、小物の破綻確認
- キャラクター同一性確認
- Inpaint等による修正
- 色、輪郭、透過、余白の確認
- レイヤー化・パーツ化への適性確認
- Referenceとの権利・類似リスク確認

### Gate C: Human Art Approval

人間が採用、不採用、修正を判断する。

人間承認前の画像へ `approved`、`final`、`production` を付けない。

---

## 5. Live2D Pipeline

目標は、人間の指示・入力を受け、AIがパーツ制作とパラメーター設計・作成まで担当することである。

### Stage L1: Source Validation

- 正面・可動方向・隠れ部分を確認する。
- 解像度、透過、色空間を確認する。
- Live2Dで必要な補完領域を洗い出す。
- キャラクターデザイン承認済みであることを確認する。

### Stage L2: Part Definition

最低限、次のPart Listを作成する。

- Face / Skin
- Hair Front / Side / Back
- Eyes / Eyebrows / Eyelashes
- Mouth Components
- Nose / Ears
- Neck / Body
- Costume Layers
- Arms / Hands
- Accessories
- Hidden Fill Areas
- Masks and Clipping Groups

実際のPart ID、左右区分、重なり順はキャラクターごとに定義する。

### Stage L3: Part Production

利用可能な工程候補：

- segmentation
- mask生成
- inpaintingによる隠れ部分補完
- レイヤー分離
- edge cleanup
- color correction
- PSDまたは対応形式への出力

SAM系処理や補助toolは候補であり、利用前に精度とライセンスを確認する。

### Stage L4: Parameter Plan

最低限、次を検討する。

- Head Angle X / Y / Z
- Eye Open / Smile / Ball X / Y
- Brow Movement
- Mouth Open / Form
- Body Angle
- Breathing
- Hair and Accessory Physics
- Required Expressions
- Required Motions

必要パラメーターはゲーム仕様に合わせて減らし、過剰な作成を避ける。

### Stage L5: Parameter Creation

AIによるCubism操作、deformer、mesh、parameter、physics作成は未検証である。

各操作を次のStatusで管理する。

- `AUTOMATED`
- `AI_ASSISTED`
- `HUMAN_REQUIRED`
- `UNVALIDATED`

実行できない操作を完了扱いにせず、人間向け手順、入力値、確認点を出力する。

### Stage L6: Live2D QA

- パーツ境界と穴
- 変形時の破綻
- 顔・髪・衣装の一貫性
- Parameter範囲
- Physicsの安定性
- 表情・Motionの意図
- Unity SDK上の表示
- 対象端末での性能
- 書出しファイルとライセンス

### Gate D: Human Live2D Approval

人間が見た目、動き、キャラクター性、ゲーム内品質を確認する。

---

## 6. UI/UX Asset Workflow

```text
Requirement
  → User Flow
  → Wireframe
  → State Definition
  → Visual Design
  → Asset Export
  → Unity Implementation
  → UX Review
  → Human Approval
```

各画面は最低限次を定義する。

- Screen ID
- Purpose
- Entry / Exit
- User Actions
- Normal / Disabled / Selected / Loading / Error states
- Text and Localization
- Resolution / Safe Area
- Asset List
- Unity Prefab / Scene
- Review Status

UI画像だけを作成し、状態や遷移を未定義のまま完了としない。

---

## 7. Storage Plan

目標配置は `Docs/10_REPOSITORY_STRUCTURE.md` を正とする。

- ComfyUI workflow：`Workflows/ComfyUI/`
- Colab notebook・起動補助：`Tools/Colab/`
- 共通資産：`Assets/Shared/`
- Referenceと権利情報：`Assets/References/`、`Assets/Licenses/`
- ゲーム固有資産：`Games/<game-id>/Assets/`
- Live2D関連：`Games/<game-id>/Assets/Live2D/`

大容量model weight、cache、一時生成物を通常のGit管理へ含めない。必要に応じてGit LFSまたは外部Storageを人間承認のもと利用し、取得方法とhashを記録する。

---

## 8. Asset Manifest

本番候補にはmanifestを作成する。

```yaml
asset_id:
game_id:
character_id:
category:
status: draft
source_inputs: []
workflow:
  file:
  version:
models: []
seed:
prompt_reference:
license:
human_approval:
outputs: []
created_at:
updated_at:
```

Promptへ秘密情報や個人情報を記載しない。

---

## 9. Quality Gates

| Gate | Reviewer | Required Result |
|---|---|---|
| Brief Gate | Human | 入力、禁止事項、用途が明確 |
| Workflow Gate | Illustrator / Technical Reviewer | 再現可能、ライセンス確認 |
| Art Gate | Human | 見た目とキャラクター品質を承認 |
| Live2D Source Gate | Live2D Reviewer | パーツと補完領域が妥当 |
| Live2D Motion Gate | Human | 動きとキャラクター性を承認 |
| Unity Gate | QA | 表示、性能、組込みを確認 |
| Release Gate | Human | 権利・品質・配信を承認 |

---

## 10. Colab Failure Recovery

- 一時保存だけに依存しない。
- workflow JSON、manifest、採用候補、ログを一定間隔で永続保存する。
- 長時間処理は小さなJobへ分ける。
- 切断後に再利用できるseedと入力を残す。
- 同じJobを無制限に自動再実行しない。
- 課金、GPU、認証、保存先の問題は人間へ報告する。
- 復旧不能な一時ファイルを正式成果物として記録しない。

---

## 11. Acceptance Criteria

Asset Pipelineの各タスクは、次を満たした場合に完了とする。

- 入力Briefと用途が明確である。
- 生成条件と使用toolを再現できる。
- ライセンスと権利確認状態が記録されている。
- 成果物とmanifestが対応している。
- 品質Gateを通過している。
- 未検証工程と人間作業が明示されている。
- 人間が最終採用を承認している。
- Unityまたは次工程で利用できる形式になっている。

---

End of Asset Pipeline.
