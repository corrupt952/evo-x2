# [Verification 3] k8s GPU Node Utilization

## Overview
Configure EVO-X2 as a GPU node in a Kubernetes cluster and run LLM containers.

## Objectives
- Achieve GPU resource management with k8s
- Verify containerized LLM service operation
- Evaluate feasibility of scalable AI infrastructure

## Verification Items

### 1. k8s Environment Setup
```bash
# Node addition with kubeadm
sudo kubeadm join <master-ip>:6443 --token <token>

# GPU device plugin installation
kubectl apply -f https://raw.githubusercontent.com/RadeonOpenCompute/k8s-device-plugin/master/k8s-ds-amdgpu-dp.yaml
```

### 2. GPU Resource Verification
```bash
# GPU node verification
kubectl get nodes -o json | jq '.items[].status.allocatable'

# GPU information display
kubectl describe node evo-x2-node | grep amd.com/gpu
```

### 3. LLM Container Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ollama-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: ollama
  template:
    metadata:
      labels:
        app: ollama
    spec:
      containers:
      - name: ollama
        image: ollama/ollama:latest
        resources:
          limits:
            amd.com/gpu: 1
        volumeMounts:
        - name: ollama-storage
          mountPath: /root/.ollama
      volumes:
      - name: ollama-storage
        persistentVolumeClaim:
          claimName: ollama-pvc
```

### 4. LLM Backend Service
```yaml
apiVersion: v1
kind: Service
metadata:
  name: llm-backend
spec:
  selector:
    app: ollama
  ports:
  - port: 11434
    targetPort: 11434
  type: ClusterIP
```

### 5. Practical Application Examples
- **Chatbot API**
  ```python
  # Create LLM backend with FastAPI
  from fastapi import FastAPI
  import requests
  
  app = FastAPI()
  
  @app.post("/chat")
  async def chat(message: str):
      # Call Ollama API
      response = requests.post(
          "http://llm-backend:11434/api/generate",
          json={"model": "qwen2:32b", "prompt": message}
      )
      return response.json()
  ```

- **Batch Processing Job**
  ```yaml
  apiVersion: batch/v1
  kind: Job
  metadata:
    name: document-analysis
  spec:
    template:
      spec:
        containers:
        - name: analyzer
          image: custom/doc-analyzer:latest
          resources:
            limits:
              amd.com/gpu: 1
        restartPolicy: Never
  ```

### 6. Performance Measurement
- Pod startup time
- GPU allocation latency
- Resource contention with multiple Pods
- Inference speed over network

## Expected Results
- Implementation method for AMD GPU management with k8s
- Containerization overhead measurement
- Production operation feasibility evaluation

## Troubleshooting
- GPU device plugin issues
- GPU access from containers
- Memory limits and OOM killer countermeasures