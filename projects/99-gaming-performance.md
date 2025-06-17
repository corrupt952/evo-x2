# 【番外編】ゲーミング性能検証（Steam/ネイティブゲーム）

## 概要
EVO-X2の40CU RDNA 3.5 iGPUを活用したゲーミング性能を検証し、AI開発の合間のリフレッシュタイムを充実させる。

## 目的
- 統合GPUでのAAA/インディーゲームの動作確認
- AI処理とゲーミングの両立可能性検証
- 仕事の合間の適切な息抜き環境構築

## システムスペック（ゲーミング視点）
- **GPU**: 40CU RDNA 3.5 (約RTX 4060相当?)
- **メモリ**: 96GB統合メモリ（VRAM共有）
- **ストレージ**: NVMe SSD推奨
- **OS**: Windows 11 / Linux (Proton)

## 検証カテゴリ

### 1. Steamゲーム
#### AAA タイトル
| ゲーム | 設定 | 目標FPS | 備考 |
|--------|------|---------|------|
| Cyberpunk 2077 | 1080p Medium | 60fps | FSR3有効 |
| Baldur's Gate 3 | 1080p High | 60fps | - |
| Hogwarts Legacy | 1080p Medium | 45fps | レイトレなし |

#### インディー/軽量ゲーム
- Hades II
- Stardew Valley  
- Factorio
- RimWorld
- Vampire Survivors

### 2. エミュレーション
- **PS3**: RPCS3
- **Switch**: Ryujinx/Yuzu後継
- **レトロ**: RetroArch

### 3. クラウドゲーミング
- Xbox Game Pass
- GeForce NOW
- ローカルストリーミング（Steamlink）

## ゲーミング中のAI活用

### 1. AIアシスタント統合
```python
# ゲーム中の音声コマンド
async def gaming_assistant():
    commands = {
        "攻略教えて": search_game_guide,
        "配信設定": setup_streaming,
        "パフォーマンス": show_fps_stats,
        "スクショ分析": analyze_screenshot
    }
```

### 2. 自動クリップ生成
- プレイハイライトの自動検出
- キルシーンの切り抜き
- 面白い瞬間のGIF化

### 3. リアルタイム翻訳
- 海外ゲームの字幕翻訳
- ボイスチャットの同時通訳
- modの説明文翻訳

## パフォーマンス最適化

### 1. メモリ割り当て
```yaml
通常時:
  LLM: 60GB
  ゲーム: 16GB
  システム: 20GB

ゲーミングモード:
  LLM: 0-30GB (バックグラウンド)
  ゲーム: 32GB
  システム: 34GB
```

### 2. 電力プロファイル
- **バランス**: AI処理優先
- **ゲーミング**: GPU優先
- **ハイブリッド**: 動的切り替え

### 3. 冷却戦略
- ゲーミング時のファンカーブ
- サーマルパッド最適化
- 外部クーラー検討

## 実用シナリオ

### 1. 仕事の合間に
- ポモドーロテクニック（25分作業→5分ゲーム）
- ビルド待ち時間の有効活用
- 昼休みのリフレッシュ

### 2. AI開発との相乗効果
- ゲームAIの動作研究
- 強化学習の実験場
- プロシージャル生成の参考

### 3. 配信・コンテンツ作成
- LLMによる実況補助
- 自動字幕生成
- ハイライト動画編集

## ベンチマーク項目

### 基本性能
- [ ] 3DMark Time Spy
- [ ] Unigine Heaven
- [ ] 各ゲームのビルトインベンチ

### 実ゲーム性能
- [ ] 平均FPS / 1% Low
- [ ] フレームタイム分析
- [ ] 入力遅延測定

### AI併用時
- [ ] バックグラウンドLLM実行時のFPS
- [ ] ゲーム中の音声認識レイテンシ
- [ ] メモリ競合の影響

## おすすめゲームリスト

### ストレス解消系
1. **DOOM Eternal**: 爽快FPS
2. **Hades**: ローグライク
3. **Beat Saber**: VR音ゲー

### じっくり系
1. **Civilization VI**: ターン制ストラテジー
2. **Cities: Skylines**: 都市建設
3. **Two Point Hospital**: 経営シミュ

### 協力プレイ
1. **It Takes Two**: 2人協力
2. **Overcooked**: パーティーゲーム
3. **Portal 2**: パズル協力

## 期待される成果
- 1080p 60fpsでの快適プレイ
- AI処理との両立
- 効率的な気分転換
- 新たなAI活用アイデアの創出