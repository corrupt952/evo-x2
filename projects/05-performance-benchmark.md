# 【大項目5】性能検証とベンチマーク（各モデル・構成の比較）

## 概要
EVO-X2上で動作する各種LLMモデルとデプロイメント構成の性能を体系的に検証し、最適な構成を明らかにする。

## 目的
- 各モデルの実測性能データ収集
- 用途別の最適モデル選定
- リソース効率の最大化
- ボトルネックの特定と改善

## 検証対象

### 1. LLMモデル
| モデル | パラメータ | VRAM使用量 | 用途 |
|--------|------------|------------|------|
| Qwen3-32B | 32B | 約30GB | 日本語・汎用 |
| DeepSeek-R1-32B | 32B | 約25GB | 推論・数学 |
| Llama 3.3-70B | 70B | 約45GB | 高度な処理 |
| Sarashina2-70B | 70B | 約45GB | 日本語特化 |

### 2. デプロイメントツール
- **Ollama**: シンプル・開発向け
- **vLLM**: 高性能・本番向け
- **LM Studio**: GUI・実験向け
- **llama.cpp**: 軽量・組み込み向け

### 3. 量子化レベル
- Q4_K_M: バランス型（推奨）
- Q5_K_M: 高品質
- Q8_0: ほぼ無劣化
- FP16: フル精度

## ベンチマーク項目

### 1. 基本性能指標
```python
class PerformanceMetrics:
    # 速度指標
    ttft: float  # Time to First Token (秒)
    tps: float   # Tokens per Second
    
    # リソース指標
    vram_usage: float  # VRAM使用量 (GB)
    cpu_usage: float   # CPU使用率 (%)
    power_draw: float  # 消費電力 (W)
    
    # 品質指標
    perplexity: float  # 困惑度
    accuracy: float    # タスク精度
```

### 2. ワークロード別測定

#### A. 短い入力→長い出力
```yaml
task: "ストーリー生成"
input: "昔々あるところに"
output_length: 2000 tokens
measure: [TTFT, TPS, 品質]
```

#### B. 長い入力→短い出力
```yaml
task: "文書要約"
input: "10ページのPDF"
output_length: 200 tokens
measure: [TTFT, 処理速度, 精度]
```

#### C. 対話型
```yaml
task: "マルチターン会話"
context: "過去10ターン保持"
measure: [レイテンシ, コンテキスト保持]
```

### 3. 並列処理性能
- 同時リクエスト数: 1, 5, 10, 20
- スループット劣化率
- レイテンシ分布

## 実装手法

### 1. 自動ベンチマークスイート
```python
# benchmark.py
async def run_benchmark_suite():
    models = ["qwen3-32b", "deepseek-r1-32b", "llama-3.3-70b"]
    tools = ["ollama", "vllm", "lm-studio"]
    
    results = {}
    for model in models:
        for tool in tools:
            results[f"{model}_{tool}"] = await benchmark_model(
                model=model,
                tool=tool,
                test_cases=load_test_cases()
            )
    
    return generate_report(results)
```

### 2. リアルタイムモニタリング
- GPU使用率・温度
- メモリ帯域幅
- 電力消費
- システムレイテンシ

### 3. 品質評価
- 日本語ベンチマーク（JGLUE）
- コーディングタスク（HumanEval）
- 推論タスク（GSM8K）
- 実用タスク（カスタム）

## 比較マトリクス

### 速度 vs 品質
```
高品質 ↑ Llama 3.3-70B (FP16)
       │ Sarashina2-70B (Q8)
       │ Qwen3-32B (Q5_K_M)
       │ DeepSeek-R1-32B (Q4_K_M)
低品質 └─────────────────────→ 高速
         遅い              速い
```

### メモリ効率
| 構成 | モデル数 | 合計VRAM | 余裕 |
|------|----------|----------|------|
| 軽量 | 3×32B Q4 | 75GB | 21GB |
| バランス | 1×70B + 1×32B | 75GB | 21GB |
| 高性能 | 2×70B FP16 | 90GB | 6GB |

## 期待される成果

### 1. 性能マップ
- 用途別の推奨構成
- トレードオフの可視化
- 最適化の指針

### 2. 運用ガイドライン
- モデル選択フローチャート
- リソース割り当て戦略
- スケーリング計画

### 3. 改善提案
- ボトルネック箇所
- チューニングポイント
- アップグレード優先順位

## 検証項目
- [ ] 全モデル×全ツールの組み合わせテスト
- [ ] 24時間連続稼働テスト
- [ ] 極限負荷テスト
- [ ] 実業務シミュレーション