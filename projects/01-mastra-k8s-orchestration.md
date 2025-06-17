# 【大項目1】Mastra + k8s マルチLLMオーケストレーション環境の構築

## 概要
k8sクラスタ上に複数のLLM Podを展開し、Mastraフレームワークを使用して異なる特性を持つLLMを協調動作させる環境を構築する。

## 目的
- 96GBメモリを活用した複数LLM同時実行
- タスクに応じた最適なLLM選択の自動化
- スケーラブルなAIエージェントシステムの実現

## 構成要素

### 1. LLMノード（EVO-X2）
- **Qwen3-32B Pod**: 日本語・汎用処理担当（約30GB使用）
- **DeepSeek-R1-32B Pod**: 推論・数学特化（約25GB使用）
- **Llama 3.3-70B Pod**: 高度な処理・レビュー（約45GB使用）

### 2. オーケストレーション層
- **Mastra Pod**: エージェント管理とワークフロー制御
- **API Gateway**: 外部からのリクエスト受付

### 3. インフラ構成
```yaml
k8sクラスタ
├── LLMノード（EVO-X2）
│   ├── ollama-namespace
│   │   ├── qwen3-deployment
│   │   ├── deepseek-deployment
│   │   └── llama-deployment
│   └── vllm-namespace（高性能API用）
│       └── vllm-deployment
│
└── アプリケーションノード
    └── mastra-namespace
        ├── mastra-deployment
        └── api-gateway
```

## 実装ステップ

### Phase 1: 基盤構築
1. k8sクラスタへのGPUオペレーター導入
2. Ollama/vLLMのHelm Chart準備
3. 各LLMモデルのPull & デプロイ

### Phase 2: Mastra統合
1. Mastraプロジェクトのセットアップ
2. 各LLM Podへの接続設定
3. マルチエージェントワークフローの実装

### Phase 3: 実用化
1. タスク別エージェントの作成
   - 文書要約エージェント
   - コードレビューエージェント
   - 翻訳エージェント
2. エージェント間協調の実装
3. 負荷分散とフェイルオーバー

## 期待される成果
- 20%のVRAM使用率で3-4個のLLM同時稼働
- タスクに応じた自動的なモデル選択
- 10-14 tok/secでの安定動作

## 検証項目
- [ ] 複数Pod間の通信レイテンシ
- [ ] メモリ使用効率
- [ ] エージェント切り替えのオーバーヘッド
- [ ] 障害時の自動復旧