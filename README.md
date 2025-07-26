# 🚀 Antomix - Universal Claude Code Proxy

[![npm version](https://badge.fury.io/js/antomix.svg)](https://badge.fury.io/js/antomix)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Node.js Version](https://img.shields.io/badge/node-%3E%3D16.0.0-brightgreen)](https://nodejs.org/)

> **Use Claude Code with ANY AI model** - OpenAI, Groq, Gemini, Local Models, OpenRouter's 100+ models, and more!

## 🎯 Why Antomix?

**Hey there! I'm [Unclecode](https://github.com/unclecode), author of [Crawl4AI](https://github.com/unclecode/crawl4ai) (![GitHub Repo stars](https://img.shields.io/github/stars/unclecode/crawl4ai?style=social) ⭐).** 

I absolutely **love Claude Code** - it's not just about the model, it's about how brilliantly developed this agentic coding assistant is. But I wanted this incredible experience with **ALL models**, not just Claude. So I built Antomix!

**The result:** A universal proxy that converts any app connecting to Anthropic to work with:
- 🔥 **Groq** (lightning fast!)
- 🌟 **OpenRouter** (100+ models)  
- 🏠 **Local models** (Ollama, LM Studio)
- 🤖 **Gemini, OpenAI, Qwen** and more

**As a result, you can run this as a proxy and convert any app connecting to Anthropic to all other models. Anyway, have fun, star it ⭐, follow me, and share your experience!**

---

## ⚡ Quick Start

### 1️⃣ Installation
```bash
npm install -g antomix
```

### 2️⃣ Set API Keys
Make sure your API keys are set in your system:
```bash
export GROQ_API_KEY="your-groq-key"           # For Groq (super fast!)
export OPENAI_API_KEY="your-openai-key"       # For OpenAI
export GEMINI_API_KEY="your-gemini-key"       # For Gemini
export OPENROUTER_API_KEY="your-or-key"       # For OpenRouter (100+ models)
```

### 3️⃣ Launch Claude Code with Any Model
```bash
# Start Claude Code with your preferred model
antomix claude --profile openrouter-qwen # [openai|groq|gemini|...]
```

> [!IMPORTANT]
> **When you exit Claude Code, the proxy automatically stops and cleans up!**

*[GIF animation would go here showing the launch process]*

### 4️⃣ Have Fun with $$ Commands
Now that you're running, try switching models on the fly! Type these directly in Claude Code:

```bash
# Switch to super-fast Groq
$$switch-profile groq

# Check what model you're using
$$status

# Switch to OpenAI 
$$switch-profile openai

# See all available profiles
$$profiles
```

> [!TIP]
> **No restart needed!** Switch between any model instantly while keeping your conversation going.

---

## ✨ Outstanding Features

<details>
<summary>🔄 <strong>Universal API Translation</strong></summary>

- **Bidirectional conversion** between Anthropic ↔ OpenAI formats
- **Streaming support** for real-time responses  
- **Tool calls** work seamlessly across providers
- **Function calling** preserved and translated
- **System messages** handled correctly

</details>

<details>
<summary>⚡ <strong>Live Model Switching</strong></summary>

Switch models **without restarting** using $ commands:

```bash
# In Claude Code, type any of these:
$$switch-profile groq          # Switch to Groq
$$switch-profile openai        # Switch to OpenAI  
$$status                       # Check current model
$$profiles                     # List all available profiles
$$help                         # Show all commands
```

</details>

<details>
<summary>📊 <strong>Advanced Features</strong></summary>

- **Request/response logging** with session tracking
- **Usage analytics** and token counting  
- **Error handling** with detailed diagnostics
- **Rate limiting** and retry logic
- **Profile management** with YAML configs
- **Hot-swap models** without restarting
- **Runtime profile switching** via $ commands
- **Model mapping overrides** on the fly
- **Bypass mode** for direct API access

</details>

<details>
<summary>🛠 <strong>Developer Friendly</strong></summary>

- **CLI tools** for easy management
- **Daemon mode** for background operation
- **Comprehensive logging** for debugging
- **Export/import** configurations

</details>

---

## 🏃‍♂️ Running as a Service

Set up Antomix to run as a background service:

### Set Environment Variable
```bash
# Point Claude Code (or any app) to Antomix
export ANTHROPIC_BASE_URL="http://localhost:3000"
```

### Start the Service
```bash
# Start Antomix with your preferred model
antomix start --profile groq --port 3000

# Check status
antomix status

# Stop when done
antomix stop
```

> [!IMPORTANT]
> **Any application that uses Anthropic's API will now use your chosen model!** No code changes needed.

---

## 📖 Detailed Documentation

<details>
<summary>🎛 <strong>Antomix CLI Commands</strong></summary>

### Service Management
```bash
antomix start [--profile <name>] [--port <port>]  # Start proxy server
antomix stop                                       # Stop server  
antomix status                                     # Show status
antomix switch <profile>                           # Switch running server profile
```

### Profile Management
```bash
antomix profiles                                   # List available profiles
antomix export <filename>                         # Export configuration
```

### Logs and Monitoring
```bash
antomix logs                                       # View recent logs
antomix logs --follow                              # Follow logs in real-time
antomix logs --level error                         # Show only error logs
antomix logs --session <id>                       # Show logs for specific session
```

### Utilities
```bash
antomix --help                                     # Show help
antomix --version                                  # Show version
```

</details>

<details>
<summary>💬 <strong>$$ Runtime Commands</strong></summary>

Use these commands directly in Claude Code or any connected application:

### Profile Management
```bash
$$switch-profile <name>        # Switch to different model
$$profiles                     # List all available profiles
$$status                      # Show current profile and status
```

### Model Configuration  
```bash
$$models                      # Show model mappings
$$map <model> <target>        # Override model mapping
$$cat-profile <name>          # Show profile configuration
```

### Utility Commands
```bash
$$bypass on/off/status        # Toggle direct API mode
$$ping                        # Test connectivity
$$help                        # Show all $ commands
$$export <filename>           # Export current config
```

</details>

---

## 🔧 Creating Custom Profiles

<details>
<summary>📝 <strong>Profile YAML Structure</strong></summary>

Profiles are stored in `config/profiles/` and follow this structure:

```yaml
# config/profiles/my-custom.yml
name: "Custom Provider"
description: "Route requests to my custom API"

# Model mappings - maps Claude models to your provider's models
models:
  "claude-opus-4-20250514": 
    - "your-best-model"
  "claude-sonnet-4-20250514": 
    - "your-balanced-model"
  "claude-3-5-haiku-20241022": 
    - "your-fast-model"

# Parameter transformations for your models
parameters:
  "*":  # All models
    "[max_tokens]": "max_completion_tokens"  # Rename parameter
    "max_completion_tokens": 4096  # Set default limit

# API configuration
api:
  base_url: "https://api.yourprovider.com/v1"
  api_key: "$YOUR_PROVIDER_API_KEY"
  headers:
    # Custom headers if needed
```

</details>

<details>
<summary>⚙️ <strong>Creating Profiles</strong></summary>

Create new profiles by:

1. **Manual Creation**: Add a new `.yml` file to `config/profiles/`
2. **Copy Existing**: Use an existing profile as a template
3. **Modify Settings**: Update API endpoints, keys, and model mappings
4. **Test Connection**: Use `$$status` to verify the profile works

Example workflow:
```bash
# 1. Copy existing profile
cp config/profiles/groq.yml config/profiles/my-provider.yml

# 2. Edit the configuration
# Update API endpoints, keys, and model mappings

# 3. Test the new profile
antomix start --profile my-provider
```

</details>

---

## 📊 Logging and Monitoring

<details>
<summary>📈 <strong>Log Commands</strong></summary>

```bash
# View recent logs
antomix logs

# Follow logs in real-time
antomix logs --follow

# Filter by log level
antomix logs --level error
antomix logs --level warn
antomix logs --level info

# View logs for a specific session
antomix logs --session <session-id>
```

**Log locations:**
- Daily logs: `~/.antomix/logs/daily/`
- Session logs: `~/.antomix/logs/sessions/`
- Error logs: `~/.antomix/logs/antomix-error-YYYY-MM-DD.log`

</details>

---

## 📋 Available Profiles

- `groq` - Groq API (super fast inference)
- `openai` - OpenAI GPT models  
- `gemini` - Google Gemini
- `openrouter-qwen` - Qwen via OpenRouter
- `openrouter-kimi` - Kimi via OpenRouter
- `default` - OpenAI GPT-4-1 and O3 by default

---

## 🤝 Contributing

Found a bug? Want a new provider? 

1. 🌟 **Star this repo**
2. 🐛 **Report issues** on GitHub  
3. 💡 **Suggest features** via discussions
4. 🔀 **Submit PRs** for improvements

---

## 📄 License

MIT License - see [LICENSE](LICENSE) file for details.

---

## 🔗 Links

- 🐙 **GitHub**: [unclecode/antomix](https://github.com/unclecode/antomix)
- 📦 **npm**: [antomix](https://www.npmjs.com/package/antomix)
- 🕷️ **Crawl4AI**: [My other project](https://github.com/unclecode/crawl4ai) ![GitHub Repo stars](https://img.shields.io/github/stars/unclecode/crawl4ai?style=social)
- 🐦 **Follow me**: [@unclecode](https://x.com/unclecode)

---

<div align="center">

**⭐ If Antomix saves you time, please star it! ⭐**

**Made with ❤️ by [Unclecode](https://github.com/unclecode)**

</div>