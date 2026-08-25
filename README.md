# AI Game Studio

> AIと人間が協調し、複数のゲームを継続制作するためのAI-first Game Development Platform

## Overview

AI Game Studioは、個人または少人数でも、AIを専門メンバーとして活用してゲームを企画・開発・検証・公開・運用できる再利用可能な制作基盤を構築するプロジェクトです。

このリポジトリは単一ゲームのリポジトリではありません。AIOS、制作ルール、Unityテンプレート、画像・Live2D・シナリオPipeline、QA、長期記憶を共通基盤として整備します。

人間が最終判断を行い、AIは承認された範囲で企画、設計、実装、デザイン、進行管理、制作、テスト、文書更新を担当します。

## Start Here

最初に [99_AI_CONTEXT.md](Docs/99_AI_CONTEXT.md) を開き、同書Section 3「Required Start Order」を正規の読込順として使用します。

READMEの役割は入口の案内であり、必須文書の一覧を置き換えるものではありません。次に [00_AI_BOOTSTRAP.md](Docs/00_AI_BOOTSTRAP.md) を読み、99で指定された共通文書、現在Taskに必要なDomain文書、実行Protocolを確認してから作業を開始してください。

現在の進捗は [04_PROJECT_STATUS.md](Docs/04_PROJECT_STATUS.md)、判断理由は [05_DECISION_LOG.md](Docs/05_DECISION_LOG.md)、再開情報は [12_SESSION_HANDOVER.md](Docs/12_SESSION_HANDOVER.md) を参照してください。

## Core Principles

- Human Final Authority
- GitHub main as Single Source of Truth
- Documentation First
- Role-Based AI Assignment
- Independent Review
- Reuse Before Create
- Reproducibility
- Small and Reversible Changes
- Long-Term Maintainability

## Project Scope

- 企画：Main Planner + Reviewer 2名による3者合議
- 開発：Unity、Firebase、WebGL-firstの検証
- デザイン：UI・UX、画面、画像パーツ
- 進行管理：Task、依存関係、Risk、引継ぎ
- キャラクター：Stable Diffusion + ComfyUI + 有料Google Colab
- Live2D：AIによるパーツ・parameter制作を目標
- シナリオ：ラノベ系文章、会話、分岐、Unity用data
- QA・Release：Independent Reviewと人間の最終承認

有料ColabのSessionは人間が開始し、稼働中にComfyUIとAIOSから操作します。GPT-Image-2とNano Banana Proは、本番キャラクターイラストの主系統として採用していません。

## Technical Baseline

| Area | Current Direction |
|---|---|
| Game Engine | Unity 6 / Unity Personal |
| Backend | Firebase |
| Early Validation | WebGL |
| Distribution | App Store / Google Play / Steam |
| Version Control / SSOT | GitHub |
| Character Image | Stable Diffusion + ComfyUI |
| Image Compute | Paid Google Colab, human-started |
| Character Animation | Live2D |
| AI Operations | AIOS + Role-Based AI + Model Registry |

詳細は [06_ARCHITECTURE.md](Docs/06_ARCHITECTURE.md) を参照してください。

## Documentation

| File | Responsibility |
|---|---|
| [00_AI_BOOTSTRAP.md](Docs/00_AI_BOOTSTRAP.md) | 起動規約、読込順、権限境界 |
| [01_PROJECT_OVERVIEW.md](Docs/01_PROJECT_OVERVIEW.md) | 目的、対象、成功条件 |
| [02_AI_ROLES.md](Docs/02_AI_ROLES.md) | Role、能力要件、担当候補 |
| [03_AI_RULES.md](Docs/03_AI_RULES.md) | 行動規則、禁止事項、承認条件 |
| [04_PROJECT_STATUS.md](Docs/04_PROJECT_STATUS.md) | 現在の進捗、Risk、Next |
| [05_DECISION_LOG.md](Docs/05_DECISION_LOG.md) | 重要判断と理由 |
| [06_ARCHITECTURE.md](Docs/06_ARCHITECTURE.md) | AIOSと技術構成 |
| [07_ASSET_PIPELINE.md](Docs/07_ASSET_PIPELINE.md) | UI、画像、Colab、Live2D |
| [08_SCENARIO_PIPELINE.md](Docs/08_SCENARIO_PIPELINE.md) | シナリオ制作・実装工程 |
| [09_QA_RELEASE_POLICY.md](Docs/09_QA_RELEASE_POLICY.md) | QAとRelease基準 |
| [10_REPOSITORY_STRUCTURE.md](Docs/10_REPOSITORY_STRUCTURE.md) | 配置、命名、Version |
| [11_PROJECT_MEMORY.md](Docs/11_PROJECT_MEMORY.md) | 長期的な知識と学習 |
| [12_SESSION_HANDOVER.md](Docs/12_SESSION_HANDOVER.md) | Session引継ぎ |
| [91_AI_EXECUTION_PROTOCOL.md](Docs/91_AI_EXECUTION_PROTOCOL.md) | AIOS実行Lifecycle |
| [92_AI_PLAYBOOK.md](Docs/92_AI_PLAYBOOK.md) | Role別実践手順 |
| [93_AI_TASK_PROTOCOL.md](Docs/93_AI_TASK_PROTOCOL.md) | 個別Taskの形式と完了条件 |
| [99_AI_CONTEXT.md](Docs/99_AI_CONTEXT.md) | 現在地と参照Dashboard |

## Repository Structure

```text
Docs/       AIOS共通文書
Games/      ゲーム別Project
Templates/  ゲーム・文書・Task Template
Workflows/  AIOS、CI、ComfyUI、Scenario workflow
Tools/      Colab、Unity、Live2D、Model Registry
Scripts/    Build、Validation、Conversion
Assets/     複数ゲームで共有するAssetと権利情報
```

詳細は [10_REPOSITORY_STRUCTURE.md](Docs/10_REPOSITORY_STRUCTURE.md) を参照してください。

## Current Status

Stage 1: Governance Foundationです。

文書体系はReview可能な状態です。Unity Template、Firebase、Colab + ComfyUI接続、Live2D自動化、Scenario変換、QA自動化は未実装または未検証です。

目標構成を実装済みと解釈しないでください。

## License

This repository is licensed under the [Apache License 2.0](LICENSE).
