# [Extra] Gaming Performance Verification (Steam/Native Games)

## Overview
Verify gaming performance utilizing EVO-X2's 40CU RDNA 3.5 iGPU to enhance refresh time between AI development.

## Objectives
- Confirm AAA/indie game operation with integrated GPU
- Verify compatibility of AI processing and gaming
- Build appropriate break environment during work

## System Specs (Gaming Perspective)
- **GPU**: 40CU RDNA 3.5 (approx. RTX 4060 equivalent?)
- **Memory**: 96GB unified memory (VRAM shared)
- **Storage**: NVMe SSD recommended
- **OS**: Windows 11 / Linux (Proton)

## Verification Categories

### 1. Steam Games
#### AAA Titles
| Game | Settings | Target FPS | Notes |
|------|----------|------------|-------|
| Cyberpunk 2077 | 1080p Medium | 60fps | FSR3 enabled |
| Baldur's Gate 3 | 1080p High | 60fps | - |
| Hogwarts Legacy | 1080p Medium | 45fps | No ray tracing |

#### Indie/Lightweight Games
- Hades II
- Stardew Valley  
- Factorio
- RimWorld
- Vampire Survivors

### 2. Emulation
- **PS3**: RPCS3
- **Switch**: Ryujinx/Yuzu successors
- **Retro**: RetroArch

### 3. Cloud Gaming
- Xbox Game Pass
- GeForce NOW
- Local streaming (Steam Link)

## AI Utilization During Gaming

### 1. AI Assistant Integration
```python
# Voice commands during gaming
async def gaming_assistant():
    commands = {
        "guide me": search_game_guide,
        "streaming setup": setup_streaming,
        "performance": show_fps_stats,
        "analyze screenshot": analyze_screenshot
    }
```

### 2. Automatic Clip Generation
- Automatic detection of play highlights
- Kill scene extraction
- GIF creation of funny moments

### 3. Real-time Translation
- Foreign game subtitle translation
- Voice chat simultaneous interpretation
- Mod description translation

## Performance Optimization

### 1. Memory Allocation
```yaml
Normal mode:
  LLM: 60GB
  Game: 16GB
  System: 20GB

Gaming mode:
  LLM: 0-30GB (background)
  Game: 32GB
  System: 34GB
```

### 2. Power Profiles
- **Balanced**: AI processing priority
- **Gaming**: GPU priority
- **Hybrid**: Dynamic switching

### 3. Cooling Strategy
- Fan curves for gaming
- Thermal pad optimization
- External cooler consideration

## Practical Scenarios

### 1. During Work Breaks
- Pomodoro technique (25min work → 5min game)
- Effective use of build wait time
- Lunch break refresh

### 2. Synergy with AI Development
- Game AI behavior research
- Reinforcement learning experimental ground
- Reference for procedural generation

### 3. Streaming/Content Creation
- LLM-assisted live commentary
- Automatic subtitle generation
- Highlight video editing

## Benchmark Items

### Basic Performance
- [ ] 3DMark Time Spy
- [ ] Unigine Heaven
- [ ] Built-in benchmarks for each game

### Real Game Performance
- [ ] Average FPS / 1% Low
- [ ] Frame time analysis
- [ ] Input lag measurement

### During AI Usage
- [ ] FPS with background LLM execution
- [ ] Voice recognition latency during gaming
- [ ] Memory contention impact

## Recommended Game List

### Stress Relief
1. **DOOM Eternal**: Exhilarating FPS
2. **Hades**: Roguelike
3. **Beat Saber**: VR rhythm game

### Relaxing
1. **Civilization VI**: Turn-based strategy
2. **Cities: Skylines**: City building
3. **Two Point Hospital**: Management sim

### Cooperative Play
1. **It Takes Two**: 2-player co-op
2. **Overcooked**: Party game
3. **Portal 2**: Puzzle co-op

## Expected Results
- Comfortable play at 1080p 60fps
- Compatibility with AI processing
- Efficient mood refreshment
- Creation of new AI utilization ideas