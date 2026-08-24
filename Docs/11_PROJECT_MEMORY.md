# Project Memory

Version: 1.0.0  
Last Updated: 2026-08-24  
Status: Active

---

## 1. Purpose

本書は、セッションをまたいで保持すべき長期的な知識、前提、制約、学習内容を記録する。

現在の進捗はProject Status、判断履歴はDecision Log、次回再開情報はSession Handoverを正とする。本書へ一時的な進捗やチャット全文を保存しない。

---

## 2. Memory Categories

### Project Identity

- プロジェクト名はAI Game Studio。
- 単一タイトルではなく、複数ゲームを継続制作・運用する再利用可能な基盤を構築する。
- 個人または少人数でのゲーム制作をAIで支援する。
- GitHubのmainを承認済み情報のSSOTとする。
- 人間が最終判断者である。

### Human Collaboration

- 人間はAIへ指示・入力を行う。
- ゲームコンセプト、創作方針、主要仕様、品質、予算、権利、公開を人間が最終承認する。
- mainへのマージ、破壊的操作、有料サービス開始は人間承認を必要とする。
- AIは未確認事項を推測で正式仕様にしない。
- 人間が理解・確認できない成果物を未確認のまま正式採用しない。

### AI Governance

- AIは役割と能力要件で選定する。
- モデル名を恒久的な役割名にしない。
- Primary、Alternative、Human Fallbackを持つ。
- 作成者とReviewerを可能な限り別モデル系統にする。
- 企画はMain Planner、Reviewer A、Reviewer Bの3者で検討する。
- 最大3ラウンドで未合意の場合は人間へ判断を求める。

### Technical Baseline

- Game EngineはUnity 6を基本とする。
- 利用条件に適合する範囲でUnity Personalを使用する。
- BackendはFirebaseを基本候補とする。
- WebGLを早期検証に使用する。
- 配信候補はApp Store、Google Play、Steam。
- GitHubで文書、コード、workflow、変更履歴を管理する。
- 外部サービスやmodelは交換可能にする。

### Character Illustration

- 本番キャラクターイラストの主系統はStable Diffusion + ComfyUI。
- GPT-Image-2とNano Banana Proは、人間の品質評価により主系統へ採用しない。
- ローカルPCに画像生成用VRAMがない。
- 有料Google ColabのVRAMを使用する。
- Colabセッションは人間が開始する。
- 稼働中にComfyUIとAIOSから操作する。
- workflow、model、LoRA、seed、prompt、主要設定を保存する。
- 生成物の最終採用は人間が判断する。

### Live2D

- 人間が指示・入力と最終確認を行う。
- AIがパーツ制作とパラメーター設計・作成まで担当することを目標とする。
- 完全自動化は未検証である。
- 工程ごとにAUTOMATED、AI_ASSISTED、HUMAN_REQUIRED、UNVALIDATEDを記録する。
- AIが実行できないCubism操作は、人間向け手順と確認点へ変換する。

### Scenario

- シナリオ制作を独立Pipelineとする。
- ラノベ系文章、会話、プロット、分岐、推敲を重視する。
- Story Bibleを設定のSSOTとする。
- プロット、本文、レビュー、実装データを分離する。
- シナリオmodelは同一条件のブラインド比較で選定する。
- 重要な物語方向と採用本文は人間が承認する。

---

## 3. Durable Lessons

### Documentation

- 会話だけに重要判断を残すと、別AI・別セッションへ正確に引き継げない。
- 1文書へ概要、役割、手順、進捗を混在させると、更新責任が不明になる。
- 文書番号を変更する場合、旧ファイルを残したままではAIが誤読する。
- 旧ファイルは削除承認までDeprecated化し、新しい参照先を明示する。
- 目標構成と実装済み状態を分けて記載する必要がある。

### AI Selection

- モデル名を固定すると、更新・廃止・価格変更でArchitectureが陳腐化する。
- 公式の性能説明だけではプロジェクト固有品質を判断できない。
- 代表タスクと同一条件による比較が必要である。
- Writer、Developer、Plannerの自己レビューだけでは偏りが残る。
- Independent Reviewerを別Providerまたは別Sessionへ分離する。

### Asset Production

- 高品質キャラクターでは、単発画像生成よりworkflow、同一性、修正、差分、Live2D適性が重要である。
- ColabはVRAM問題を解決するが、セッション切断と一時保存のRiskがある。
- seedだけでは再現できないため、model、LoRA、workflow、入力、Versionも必要である。
- Reference、Draft、Approvedを分離する必要がある。

### Live2D

- パーツ画像生成とCubism上のModel作成は別の能力である。
- 「AIがLive2Dを作れる」という一文では、実行可能範囲を判断できない。
- 工程と操作を分解し、人間操作が必要な箇所を検証する必要がある。
- Unity上の表示とPerformanceまで確認して初めてゲーム利用可能となる。

### Operations

- 有料処理はHuman-StartedまたはHuman-Approvedとして区別する。
- 外部サービスは切断・停止・規約変更を前提にFallbackを持つ。
- 同じ失敗を無制限に再試行しない。
- 完了報告にはEvidence、未確認範囲、次の復旧点が必要である。

---

## 4. Known Capability Gaps

- Antigravity 2.0でAIOS全体を運用する接続・権限・workflow
- Unity CLI / MCP / Computer Useによる安定操作
- FirebaseとGitHub Actionsの安全な接続
- Colab上のComfyUIをAIOSから操作する方法
- Stable Diffusion系modelとLoRAの品質・ライセンス評価
- Live2Dパーツ自動生成の精度
- Live2D Cubismでのparameter、deformer、mesh自動作成
- ラノベ系Scenario Writerの比較評価
- シナリオからUnityデータへの変換schema
- WebGL、Mobile、Steamの自動QA

Capability Gapは、検証完了までActive Capabilityとして扱わない。

---

## 5. Stable Facts vs. Current State

本書へ保存する：

- 長期的な目的
- 人間の恒久的な承認境界
- 採用済みの制作方針
- 再発しやすい失敗と学習
- 交換可能にすべき要素
- 検証が必要な構造的課題

本書へ保存しない：

- 今日の作業内容
- 一時的なBranch名
- 直近のNext Task
- 一時的な障害
- モデルの一時的な価格
- 長い会話ログ
- 未承認の提案

---

## 6. Memory Promotion Rules

新しい情報をProject Memoryへ追加する条件：

1. 複数の将来タスクで再利用する。
2. 別AIまたは別セッションが知らないと同じ失敗を繰り返す。
3. 一時的な進捗ではない。
4. FACTまたはACCEPTED Decisionである。
5. 権利、秘密、個人情報の問題がない。
6. 責任文書に詳細がある場合は参照に留める。

未承認の仮説を永続記憶へ昇格しない。

---

## 7. Memory Entry Template

```markdown
### M-XXX: Title

- Date:
- Status: FACT | ACCEPTED | SUPERSEDED
- Category:
- Memory:
- Why It Matters:
- Evidence / Decision:
- Related Files:
- Review Date:
```

古いMemoryは削除せず、SUPERSEDEDと後継参照を記録する。

---

## 8. Review Cadence

Project Memoryは次のタイミングで確認する。

- 重要な失敗または復旧後
- 新しいGameを開始する前
- AIモデルまたは主要toolを変更する時
- Architectureを変更する時
- Release後の振返り
- 同じ問題が2回発生した時

---

End of Project Memory.
