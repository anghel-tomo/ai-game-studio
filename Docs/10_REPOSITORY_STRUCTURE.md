# Repository Structure

Version: 1.0.0  
Last Updated: 2026-08-24  
Status: Active Design / Migration Pending

---

## 1. Purpose

本書は、AI Game Studioのフォルダ構成、配置責務、命名規則、Version管理、禁止事項を定義する。

現在は多くのフォルダが `.gitkeep` のみである。本書は目標構成を示し、存在しないフォルダやファイルを実装済みと扱わない。

---

## 2. Top-Level Structure

```text
/
├─ .github/
├─ Assets/
├─ Docs/
├─ Games/
├─ Scripts/
├─ Templates/
├─ Tools/
├─ Workflows/
├─ .gitignore
├─ LICENSE
└─ README.md
```

Top-Levelフォルダの追加、削除、名称変更はArchitecture変更として扱い、人間承認とDecision Log更新を必要とする。

---

## 3. Target Structure

```text
/
├─ .github/
│  ├─ ISSUE_TEMPLATE/
│  ├─ workflows/
│  └─ PULL_REQUEST_TEMPLATE.md
├─ Assets/
│  ├─ Shared/
│  ├─ References/
│  └─ Licenses/
├─ Docs/
│  ├─ 00_AI_BOOTSTRAP.md
│  ├─ 01_PROJECT_OVERVIEW.md
│  ├─ 02_AI_ROLES.md
│  ├─ 03_AI_RULES.md
│  ├─ 04_PROJECT_STATUS.md
│  ├─ 05_DECISION_LOG.md
│  ├─ 06_ARCHITECTURE.md
│  ├─ 07_ASSET_PIPELINE.md
│  ├─ 08_SCENARIO_PIPELINE.md
│  ├─ 09_QA_RELEASE_POLICY.md
│  ├─ 10_REPOSITORY_STRUCTURE.md
│  ├─ 11_PROJECT_MEMORY.md
│  ├─ 12_SESSION_HANDOVER.md
│  ├─ 91_AI_EXECUTION_PROTOCOL.md
│  ├─ 92_AI_PLAYBOOK.md
│  ├─ 93_AI_TASK_PROTOCOL.md
│  └─ 99_AI_CONTEXT.md
├─ Games/
│  └─ <game-id>/
│     ├─ README.md
│     ├─ Docs/
│     ├─ Unity/
│     ├─ Assets/
│     │  ├─ Art/
│     │  ├─ UI/
│     │  └─ Live2D/
│     ├─ Scenario/
│     │  ├─ Bible/
│     │  ├─ Plot/
│     │  ├─ Drafts/
│     │  ├─ Approved/
│     │  ├─ Data/
│     │  └─ Reviews/
│     ├─ Tests/
│     └─ Releases/
├─ Scripts/
│  ├─ Build/
│  ├─ Validation/
│  └─ Conversion/
├─ Templates/
│  ├─ Game/
│  ├─ Unity/
│  ├─ Documents/
│  ├─ Tasks/
│  ├─ Manifests/
│  └─ Scenario/
├─ Tools/
│  ├─ Colab/
│  ├─ Live2D/
│  ├─ ModelRegistry/
│  │  └─ AI_MODEL_REGISTRY.yaml
│  ├─ Unity/
│  └─ Validation/
└─ Workflows/
   ├─ AIOS/
   ├─ CI/
   ├─ ComfyUI/
   └─ Scenario/
```

---

## 4. Folder Responsibilities

### `.github/`

GitHub上の共同作業と自動化を管理する。

- Issue Template
- Pull Request Template
- GitHub Actions
- Code Review設定

秘密情報はworkflowへ直接記載せず、GitHub Secretsを利用する。

### `Assets/`

複数ゲームで共有する資産、参考資料、権利情報を管理する。

- `Shared/`：再利用可能な正式資産
- `References/`：参考資料。正式資産と分離
- `Licenses/`：出典、権利、利用条件

ゲーム固有資産は `Games/<game-id>/Assets/` に置く。

### `Docs/`

AI Game Studio全体のガバナンス、共通仕様、状態、運用手順を管理する。

特定ゲームの詳細仕様を混在させない。

### `Games/`

ゲームごとに独立した成果物を管理する。

各ゲームは固有のREADME、Docs、Unity、Assets、Scenario、Tests、Releasesを持つ。

### `Scripts/`

人間またはCIから再実行できるスクリプトを管理する。

- Build
- Validation
- Conversion
- Migration

一時的な実験スクリプトを説明なしに残さない。

### `Templates/`

新しいゲームやタスクで複製して使用するテンプレートを管理する。

- Game Project
- Unity
- Documents
- Task
- Manifest
- Scenario

テンプレート変更は既存ゲームへ自動適用しない。Migrationを明示する。

### `Tools/`

開発・制作を支援するtool、notebook、設定を管理する。

- Colab notebook
- Live2D補助
- Model Registry
- Unity操作補助
- Validator

外部tool本体や大容量modelを無条件で含めない。

### `Workflows/`

機械可読なworkflowと自動化定義を管理する。

- AIOS
- CI
- ComfyUI JSON
- Scenario Conversion

workflowにはVersion、依存model、入力、出力、利用条件を記載する。

---

## 5. Game Directory Rules

`<game-id>`は英小文字、数字、ハイフンで構成する。

例：

```text
Games/cafe-story-01/
```

各ゲームの `README.md` に最低限次を記載する。

- Game Name / ID
- Status
- Concept
- Target Platform
- Unity Version
- Backend
- Asset / Scenario Location
- Build Method
- Human Owner
- Current Task
- Related Decisions

ゲーム固有の重要判断はゲーム内Decision Logまたは共通Decision Logの参照を持つ。

---

## 6. Naming Rules

### Files

- 共通文書：`NN_UPPER_SNAKE_CASE.md`
- 通常文書：意味が明確な `UPPER_SNAKE_CASE.md` またはプロジェクト規約
- ID管理ファイル：英数字、`snake_case`
- ComfyUI workflow：`<purpose>_v<major>.<minor>.<patch>.json`
- Colab notebook：`<purpose>_v<major>.<minor>.<patch>.ipynb`
- Manifest：`<asset-or-task-id>.yaml`
- Unity asset：Unityの命名規則と既存プロジェクト規約を優先

### Directories

- Top-Level：PascalCase
- `<game-id>`：lower-kebab-case
- Unity内部：Unityプロジェクトの規約に従う
- OS依存の大文字小文字差を避ける

---

## 7. Version Rules

文書はSemantic Versioningを使用する。

workflow、template、schemaは互換性を意識してVersionを付ける。

- Major：互換性のない変更
- Minor：後方互換の機能追加
- Patch：修正・明確化

日付や `latest` だけで正式Versionを表さない。必要な場合はVersionと日付を併記する。

生成物の全候補へVersionを付ける必要はない。正式採用候補と再利用対象を優先する。

---

## 8. Large File Policy

通常のGit管理へ次を含めない。

- Stable Diffusion等のmodel weight
- 大量の生成途中画像
- Build cache
- Unity Library
- Colab cache
- 一時動画
- 秘密情報
- 再生成可能な巨大中間ファイル

必要な大容量資産は、次のいずれかを人間承認のもと使用する。

- Git LFS
- 外部Storage
- Release Artifact
- Package Registry

リポジトリには取得先、Version、hash、License、再現手順を残す。

---

## 9. Secret and Local File Policy

- `.env`、token、key、credentialをコミットしない。
- サンプルは `.env.example` のように値を除いて保存する。
- Unityのユーザー固有設定、OS固有設定、cacheを除外する。
- Colabの認証出力とmount情報を残さない。
- Secretが混入した場合は、削除だけでなく失効・再発行を人間へ依頼する。

---

## 10. Document Migration

最終構成では次を使用する。

- `Docs/02_AI_ROLES.md`
- `Docs/03_AI_RULES.md`
- `Docs/04_PROJECT_STATUS.md`
- `Docs/12_SESSION_HANDOVER.md`

旧文書：

- `Docs/02_AI_RULES.md`
- `Docs/03_PROJECT_STATUS.md`
- `Docs/04_SESSION_HANDOVER.md`

旧文書は新文書への参照だけを残してDeprecated化する。削除は人間の明示的な承認後に行う。

---

## 11. Structure Change Process

1. 変更理由を明確にする。
2. 影響する文書、workflow、script、CI、ゲームを検索する。
3. 移行先とRollbackを定義する。
4. Architectがレビューする。
5. 人間が承認する。
6. 作業ブランチで小さく変更する。
7. 参照先とREADMEを更新する。
8. Decision Logへ記録する。
9. 人間承認後にmainへマージする。

---

## 12. Acceptance Criteria

- 各ファイルが責任フォルダに置かれている。
- 共有資産とゲーム固有資産が分離されている。
- Reference、Draft、Approvedが区別されている。
- 大容量ファイルと秘密情報が除外されている。
- Version、License、取得方法を追跡できる。
- 文書リンクと番号に競合がない。
- 新しいTop-Level追加が承認されている。

---

End of Repository Structure.
