# [Verification 1] Ubuntu Server Setup on EVO-X2

## Overview
Install Ubuntu Server 24.04 on EVO-X2 and establish a basic environment for running LLMs with ROCm.

## Objectives
- Establish Windows environment backup procedure
- Verify ROCm operation on Ubuntu 24.04
- Confirm basic LLM operation with Ollama/LM Studio

## Verification Items

### 1. Windows Recovery Disk Preparation
- How to obtain recovery image from GMKtec official site
- Download Windows 11 official ISO
- Recovery USB creation procedure

### 2. Ubuntu Server 24.04 Installation
- Disable Secure Boot in BIOS
- Installation considerations
- Driver recognition status check

### 3. ROCm Environment Setup
```bash
# ROCm 6.x installation procedure
wget https://repo.radeon.com/amdgpu-install/latest/ubuntu/jammy/amdgpu-install_6.x.x-1_all.deb
sudo apt-get update
sudo apt-get install ./amdgpu-install_6.x.x-1_all.deb
sudo amdgpu-install --usecase=rocm
```

### 4. Ollama Installation and Operation Verification
```bash
# Ollama installation
curl -fsSL https://ollama.com/install.sh | sh

# GPU recognition check
ollama list

# Test model execution
ollama run qwen2:32b-instruct-q4_K_M
```

### 5. Performance Measurement
- Model loading time
- TTFT (Time to First Token)
- TPS (Tokens per Second)
- Memory usage

## Expected Results
- Confirmation of ROCm operation on Ubuntu 24.04
- Performance comparison data with Windows
- Setup procedure documentation

## Troubleshooting
- Solutions for GPU not recognized
- ROCm installation error resolution
- Performance issue investigation procedures

## References
- [AMD ROCm Documentation](https://rocm.docs.amd.com/)
- [Ollama Documentation](https://ollama.com/docs)
- [Ubuntu Server Guide](https://ubuntu.com/server/docs)