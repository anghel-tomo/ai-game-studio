# Project Overview

Version: 1.0

---

# 1. Project Vision

## AI-First Game Studio

本プロジェクトは、AIを開発チームの一員として活用する
次世代型ゲーム開発基盤（AI Game Studio）を構築することを目的とする。

従来のゲーム開発では、人間の開発者が中心となり、
AIは補助ツールとして利用されてきた。

本プロジェクトではその概念を拡張し、
AIエージェントが企画、設計、実装、検証、改善までの
開発プロセス全体に参加する環境を構築する。

人間は最終判断者として、
ゲーム品質、方向性、ビジネス判断を担当する。

---

# 2. Project Purpose

本プロジェクトの目的は、
単一タイトルを制作することではない。

AIと人間が協調することで、
継続的に複数タイトルを開発可能な
ゲーム開発オペレーションシステムを構築することである。

目標:

- 開発期間の短縮
- 開発コスト削減
- 開発工程の自動化
- AIによる品質改善
- 開発ノウハウの再利用
- 少人数でも高品質なゲーム制作を可能にする

---

# 3. Core Philosophy

## 3.1 AI is a Team Member

AIは単なる生成ツールではなく、
専門領域を持った開発メンバーとして扱う。

例:

- AI Producer
- AI Game Designer
- AI Programmer
- AI Artist Assistant
- AI QA Engineer
- AI Analyst

各AIは明確な役割と責任範囲を持つ。

---

## 3.2 Human Makes Final Decisions

AIは提案・生成・分析を担当する。

最終判断は人間が行う。

人間の責任:

- ゲームコンセプト決定
- 品質判断
- 仕様承認
- リリース判断
- ビジネス判断

---

## 3.3 Documentation First

AI開発では、
情報共有と履歴管理が重要になる。

そのため本プロジェクトでは、

- 仕様
- 設計
- 判断理由
- 開発ルール
- 進行状況

をドキュメントとして管理する。

ドキュメントはAIと人間双方の共通認識となる。

---

## 3.4 GitHub as Single Source of Truth

GitHubをプロジェクトの唯一の正しい情報源（Single Source of Truth）とする。

管理対象:

- ソースコード
- 仕様書
- AI向け指示書
- 開発ルール
- タスク管理情報
- 変更履歴

ローカル環境や個人チャット内だけに存在する情報は、
正式なプロジェクト情報とは扱わない。

---

# 4. Development Strategy

## Phase 1: AI Assisted Development

人間主体の開発にAIを導入する。

目的:

- AI活用方法の確立
- 開発効率向上
- AI品質確認

---

## Phase 2: AI Collaborative Development

AIが専門担当として開発工程へ参加する。

対象:

- 企画生成
- 仕様書作成
- タスク分解
- コード生成
- テスト作成
- 改善提案

---

## Phase 3: AI Operating Studio

AIエージェント群による
継続的ゲーム開発環境を構築する。

目標:

- 複数タイトル同時開発
- AIによる開発管理
- AIによる運用改善
- 再利用可能な開発システム

---

# 5. Target Products

初期開発対象:

- カジュアルスマートフォンゲーム

想定プラットフォーム:

- iOS
- Android
- Steam

検証環境:

- WebGL

---

# 6. Technical Foundation

## Game Engine

Unity Personal

用途:

- ゲームクライアント開発
- UI実装
- ゲームロジック
- クロスプラットフォーム対応

---

## Backend

候補:

- Firebase
- PlayFab

用途:

- ユーザーデータ管理
- 認証
- リアルタイムイベント
- 分析

---

## Version Control

GitHub

役割:

- ソースコード管理
- ドキュメント管理
- AI連携基盤
- 開発履歴管理

---

## Character / Art Pipeline

必要に応じて:

- Live2D
- AI画像生成
- AI補助デザイン

を利用する。

---

# 7. AI Development Roles

AIは以下の役割単位で管理する。

## AI Producer

担当:

- プロジェクト管理
- 優先順位判断補助
- 仕様整理
- リスク管理

---

## AI Game Designer

担当:

- ゲーム企画
- システム設計
- バランス設計
- UX改善

---

## AI Programmer

担当:

- コード生成
- リファクタリング
- 技術調査
- 実装補助

---

## AI QA Engineer

担当:

- テスト設計
- バグ分析
- 品質確認

---

## AI Analyst

担当:

- データ分析
- KPI分析
- 改善提案

---

# 8. Development Rules

本プロジェクトでは以下を基本ルールとする。

1. すべての重要判断はドキュメント化する

2. AI生成物は必ずレビューする

3. 理解できないコードや仕様は採用しない

4. 小さな改善を継続する

5. 再利用可能な仕組みを優先する

---

# 9. Success Criteria

本プロジェクトの成功条件:

## Development

- AIを利用してゲーム制作工程を短縮できる
- 少人数で開発可能になる
- 開発ノウハウを再利用できる

## AI System

- AIエージェントが役割分担して動作する
- 新規タイトルでも同じ基盤を利用できる
- AI開発プロセスが改善され続ける

## Business

- 継続的にゲームタイトルをリリースできる
- 開発コストに対して十分な収益性を確保できる

---

# 10. Project Long-Term Goal

最終目標は、
「AIを活用したゲーム制作」ではない。

AIと人間が協調し、
継続的にゲームを生み出す
AI Game Studioを構築することである。

このリポジトリは、
そのための開発基盤・知識基盤・運用基盤となる。
