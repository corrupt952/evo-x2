# EVO-X2 Ubuntu Environment Verification Project Overview

## Background
Most existing EVO-X2 reviews focus on Windows environments, lacking real-world data for Ubuntu setups.
Nobody has verified the performance of 96GB memory for LLM execution or Linux-specific tools.

## Verification Projects

### [Verification 1] Ubuntu Server Setup
**File**: [01-ubuntu-setup-rocm.md](./01-ubuntu-setup-rocm.md)
- Windows recovery disk preparation
- Ubuntu 24.04 + ROCm environment setup
- Basic operation verification with Ollama/LM Studio

### [Verification 2] Whisper Speech Recognition
**File**: [02-whisper-verification.md](./02-whisper-verification.md)
- Whisper operation verification in ROCm environment
- Speech recognition accuracy and real-time performance evaluation
- Practical voice input system construction

### [Verification 3] k8s GPU Node
**File**: [03-k8s-gpu-node.md](./03-k8s-gpu-node.md)
- Configure EVO-X2 as k8s cluster GPU node
- LLM container deployment and operation
- Application backend utilization

### [Verification 4] Dify/n8n Workflow
**File**: [04-dify-n8n-workflow.md](./04-dify-n8n-workflow.md)
- LLM utilization with no-code tools
- Practical automation workflow implementation
- AI business system in fully local environment

### [Extra] Gaming Performance
**File**: [99-gaming-performance.md](./99-gaming-performance.md)
- Game operation verification with 40CU iGPU
- Refresh environment between AI development

## Test Environment
- **Hardware**: GMKtec EVO-X2 (AMD Ryzen AI Max+ 395)
- **Memory**: 96GB LPDDR5X
- **OS**: Ubuntu Server 24.04 LTS
- **GPU Driver**: ROCm 6.x

## Deliverables
- Detailed procedure documentation for each verification
- Performance measurement data
- Troubleshooting guide
- Practical sample code