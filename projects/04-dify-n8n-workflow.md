# [Verification 4] Dify/n8n Practical Workflow Construction

## Overview
Run Dify and n8n on EVO-X2 to build business automation workflows utilizing local LLMs.

## Objectives
- Verify LLM utilization with no-code/low-code tools
- Implement practical automation workflows
- Build AI business systems in fully local environment

## Verification Items

### 1. Dify Setup
```bash
# Launch with Docker Compose
git clone https://github.com/langgenius/dify.git
cd dify/docker
cp .env.example .env

# Configure Ollama connection
# Edit .env file to set Ollama endpoint

docker-compose up -d
```

### 2. n8n Setup
```bash
# Launch n8n Docker image
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v n8n_data:/home/node/.n8n \
  n8nio/n8n
```

### 3. Practical Workflow Examples

#### A. Document Processing System (Dify)
```yaml
Workflow Name: Contract Review Assistant
Process Flow:
  1. PDF upload
  2. Text extraction
  3. Important clause extraction by LLM
  4. Risk assessment
  5. Report generation
```

#### B. Email Auto-Response System (n8n)
```json
{
  "nodes": [
    {
      "name": "Gmail Trigger",
      "type": "n8n-nodes-base.gmailTrigger",
      "parameters": {
        "filters": ["label:needs-response"]
      }
    },
    {
      "name": "LLM Analysis",
      "type": "n8n-nodes-base.httpRequest",
      "parameters": {
        "url": "http://localhost:11434/api/generate",
        "method": "POST",
        "body": {
          "model": "qwen2:32b",
          "prompt": "Analyze email and create response: {{$json.text}}"
        }
      }
    }
  ]
}
```

#### C. Meeting Minutes Generation (Dify + Whisper)
```yaml
Workflow Name: Meeting Recording Automation
Process Flow:
  1. Audio file upload
  2. Transcription with Whisper
  3. Summary and formatting by LLM
  4. Action item extraction
  5. Automatic distribution to participants
```

#### D. Data Analysis Report Generation (n8n)
```yaml
Workflow Name: Weekly Sales Analysis
Process Flow:
  1. Retrieve sales data from database
  2. Trend analysis by LLM
  3. Anomaly detection and cause estimation
  4. Graph generation
  5. Report posting to Slack
```

### 4. Performance Evaluation
- Workflow execution time
- Number of concurrent workflows
- Memory usage trends
- Error rate and stability

### 5. Implementation Points
```javascript
// n8n custom node example
module.exports = {
  description: {
    displayName: 'Local LLM',
    name: 'localLlm',
    properties: [
      {
        displayName: 'Model',
        name: 'model',
        type: 'options',
        options: [
          { name: 'Qwen 32B', value: 'qwen2:32b' },
          { name: 'Llama 70B', value: 'llama3.3:70b' }
        ]
      }
    ]
  },
  async execute() {
    // Call Ollama API
  }
}
```

## Expected Results
- Business automation utilizing local LLMs
- Document processing system with privacy protection
- Introduction and operational cost estimation

## Security Considerations
- Network isolation configuration
- Access control
- Data encryption
- Audit log configuration