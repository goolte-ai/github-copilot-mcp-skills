```
Complete Custom Model Provider Methods for GitHub Copilot
Production README for VS Code + Jira/Splunk Skills
All methods to register custom LLMs (Azure AI, OpenRouter, Ollama VM, etc.) in Copilot Chat model picker.

📋 Table of Contents
Method 1: Custom LLM Provider Extension

Method 2: Native VS Code settings.json

Method 3: GitHub Enterprise BYOK

Method 4: Continue.dev Extension

Method 5: Ollama Remote VM

Provider Templates

Testing

Method 1: Custom LLM Provider Extension (Recommended)
Fastest setup - works with ANY OpenAI-compatible endpoint.

Install & Setup
text
1. VS Code Extensions → "Custom LLM Provider" → Install
2. Ctrl+Shift+P → "Custom LLM: Add Provider"
3. Fill form:
Name: "Zensar Qwen"
Base URL: https://openrouter.ai/api/v1
API Key: or_sk-yourkey

text
4. Ctrl+Shift+P → "Custom LLM: Refresh Models"
5. Copilot Chat → Model picker → Your model ✓
Pros: 100+ models, no settings.json, works immediately
Cons: Extension dependency

Method 2: Native VS Code settings.json (No Extension)
Zero extensions - pure VS Code configuration.

settings.json Config
text
Ctrl+Shift+P → "Preferences: Open Settings (JSON)"
json
{
  "github.copilot.chat.experimental.azureModels": {
    "zensar-openrouter": {
      "name": "Zensar OpenRouter Qwen",
      "url": "https://openrouter.ai/api/v1/chat/completions",
      "maxInputTokens": 131072,
      "maxOutputTokens": 8192,
      "toolCalling": true
    },
    "zensar-azure": {
      "name": "Zensar Azure GPT-4o", 
      "url": "https://zensar.openai.azure.com/openai/deployments/gpt-4o/chat/completions?api-version=2024-02-15-preview",
      "maxInputTokens": 128000,
      "toolCalling": true
    }
  }
}
Authentication (Environment Variables)
bash
# Terminal (permanent)
export OPENROUTER_API_KEY=or_sk-yourkey
export AZURE_OPENAI_API_KEY=sk-proj-yourkey

# Reload VS Code → Model picker shows your models
Pros: No extensions, enterprise compliant
Cons: Manual env var setup

Method 3: GitHub Enterprise BYOK (Org-wide)
Admin-only - makes models available to entire organization.

text
GitHub.com → Enterprise → Copilot → Custom Models
1. Add provider: OpenAI / Anthropic / Azure AI
2. Enter YOUR API keys
3. Org-wide: All devs get your models in VS Code
4. VS Code auto-syncs (no local config needed)
Pros: Zero client config, centralized billing
Cons: Enterprise admin required

Method 4: Continue.dev Extension (Advanced)
Full IDE replacement for Copilot with 1000+ model support.

text
1. Extensions → "Continue" → Install
2. ~/.continue/config.json:
```json
{
  "models": [
    {
      "title": "Zensar Ollama VM",
      "provider": "openai",
      "model": "qwen2.5-coder:7b",
      "apiKey": "none",
      "apiBase": "http://10.0.0.50:11434/v1"
    }
  ]
}
```
3. Ctrl+L → Continue chat → Your models
Pros: Most models, local-first
Cons: Replaces Copilot Chat (different UX)

Method 5: Ollama Remote VM (Self-hosted)
100% Zensar infrastructure - zero cloud costs.

VM Setup
bash
# On VM (Ubuntu)
curl -fsSL https://ollama.com/install.sh | sh
ollama pull qwen2.5-coder:7b
sudo systemctl edit ollama.service
text
[Service]
Environment="OLLAMA_HOST=0.0.0.0:11434"
bash
sudo systemctl restart ollama
sudo ufw allow 11434/tcp
VS Code Config (settings.json)
json
{
  "github.copilot.chat.experimental.azureModels": {
    "zensar-ollama-vm": {
      "name": "Zensar Ollama VM",
      "url": "http://10.0.0.50:11434/v1/chat/completions",
      "maxInputTokens": 32768,
      "toolCalling": true
    }
  }
}
Pros: Zero cost, full control, air-gapped capable
Cons: VM management overhead

Provider Templates (Copy-Paste Ready)
Provider	settings.json URL	Environment Variable
OpenRouter	https://openrouter.ai/api/v1/chat/completions	OPENROUTER_API_KEY
Azure OpenAI	https://your-resource.openai.azure.com/...	AZURE_OPENAI_API_KEY
Anthropic	https://api.anthropic.com/v1/messages	ANTHROPIC_API_KEY
Ollama VM	http://VM-IP:11434/v1/chat/completions	None
LM Studio	http://localhost:1234/v1/chat/completions	None
Testing Your Setup
text
1. Reload VS Code (Ctrl+Shift+P → "Developer: Reload Window")
2. Copilot Chat → Model dropdown → Your model ✓
3. Test Jira/Splunk skills:
   /jira-cli JIRA-123                    ✓
   /incident-orchestrator JIRA-456       ✓
4. Status bar shows: "Using Zensar Ollama VM"
Troubleshooting
Issue	Method	Fix
Model missing	All	Ctrl+Shift+P → Developer: Reload Window
401 Unauthorized	1,2	Check echo $OPENROUTER_API_KEY
Connection refused	5	VM: OLLAMA_HOST=0.0.0.0, port 11434 open
No tool calling	All	Ensure "toolCalling": true
Production Zensar Config (Complete settings.json)
json
{
  "github.copilot.chat.experimental.azureModels": {
    "zensar-openrouter": {
      "name": "Zensar OpenRouter Qwen2.5",
      "url": "https://openrouter.ai/api/v1/chat/completions",
      "maxInputTokens": 131072,
      "toolCalling": true
    },
    "zensar-ollama-vm": {
      "name": "Zensar Ollama VM (Prod)",
      "url": "http://ollama.corp.zensar.com:11434/v1/chat/completions", 
      "maxInputTokens": 32768,
      "toolCalling": true
    }
  }
}
🚀 Deploy any method → Your Jira/Splunk skills work immediately!

text
Pick method → Copy config → Reload VS Code → /incident-orchestrator JIRA-123 → LIVE!
Perfect for Zensar enterprise - BYOK compliance, zero vendor lock-in, full MCP support.
```
