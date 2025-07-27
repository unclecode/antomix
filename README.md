# 🚀 Antomix - Universal **Claude Code** Proxy | Bidirectional Anthropic ↔ OpenAI API Bridge

[![npm version](https://img.shields.io/npm/v/antomix.svg)](https://www.npmjs.com/package/antomix)
[![License: TBD](https://img.shields.io/badge/License-TBD-orange.svg)](#)
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
Make sure your API keys are set in your system ([How to get API keys](#-how-to-get-api-keys)):
```bash
export GROQ_API_KEY="your-groq-key"           # For Groq (super fast!)
export OPENAI_API_KEY="your-openai-key"       # For OpenAI
export GEMINI_API_KEY="your-gemini-key"       # For Gemini
export OPENROUTER_API_KEY="your-or-key"       # For OpenRouter (100+ models)
```

### 2.5️⃣ Local Models Setup (Optional)
For **Ollama** (default local model profile):
```bash
# Install Ollama first: https://ollama.ai
ollama pull qwen:8b                           # Download the model
# No API key needed - Antomix auto-detects localhost!
```

> **⚠️ Local Model Performance Note:**
> Claude Code sends long system prompts, tools, and large context windows. This may push your GPU to its limits 🔥. Performance depends entirely on your hardware. **LM Studio** and **vLLM** profiles coming soon!

### 3️⃣ Launch Claude Code with Any Model
```bash
# Interactive selection - choose with arrow keys ✅/❌ indicators
antomix claude

# Or specify profile directly  
antomix claude --profile openrouter-qwen # [openai|groq|gemini|...]
```

> **💡 Tip:** Use `antomix profiles` to list all available profiles. Missing API keys? Antomix guides you through setup!

> [!IMPORTANT]
> **When you exit Claude Code, the proxy automatically stops and cleans up!**

*[GIF Here I will add a video or GIF animation to show how it works]*

### 4️⃣ `$$set` Command - Use Any Model for Single Messages

Switch models temporarily for individual messages without changing your main profile:

```bash
# Using shortcuts (25+ pre-configured)
$$set:gqw What's the capital of France?
$$set:o3pro Solve this complex problem: [problem]  
$$set:grok4 Write a funny story about AI
$$set:olqw Local model response

# Using direct profile/model syntax
$$set:groq/llama-3.3-70b-versatile Explain quantum computing
$$set:openai/o3-pro Analyze this code: [code]
$$set:openrouter-qwen/anthropic/claude-opus-4 Deep analysis needed
```

**Available shortcuts:**
- **Groq**: `gqw` `gll` `gdp` `gkm` (fast inference)
- **OpenAI**: `o3pro` `o3` `o4` `gpt41` (latest models) 
- **OpenRouter**: `oqw` `ogmp` `omsm` `grok4` (100+ models)
- **Anthropic**: `opu4` `sonnet4` `haiku35` (Claude models)

Manage profiles and system settings:

```bash
$$switch-profile groq          # Switch main profile to Groq
$$status                       # Check current model and status
$$shortcuts                    # List and manage shortcuts  
$$profiles                     # See all available profiles
```

> [!TIP]
> **`$$set` is temporary, `$$switch-profile` is permanent!** Use `$$set` for one-off messages, `$$switch-profile` to change your main model.

---

## 🤝 Collaborative AI - Query Multiple Models Simultaneously

**Get diverse perspectives from multiple AI models in one shot!** The `$$colab` command lets you query several models in parallel and see all their responses together.

```bash
# Ask multiple models for help debugging
$$colab o3,gpt41,oqw,grok4 Why is my Redis connection timing out in production?

# Get creative ideas from different AI perspectives  
$$colab gpt41,ogmp,sonnet4,grok4 Write a catchy marketing tagline for an eco-friendly water bottle

# Compare solutions from various models
$$colab o3,oqwt,gdp,gll What's the most efficient sorting algorithm for partially sorted data?

# Use 'fresh' to exclude conversation history for unbiased responses
$$colab oqw,o3pro,sonnet4 fresh Review this architecture without context
```

**How it works:**
- List models separated by commas (NO spaces: `o3,gpt41,gll` ✅ not `o3, gpt41, gll` ❌)
- Models execute in parallel - if one fails, others still respond
- See all responses in one organized view

> [!TIP]
> Check the detailed docs below for pre-configured model sets like `think`, `code`, and `docs` that group the best models for specific tasks!

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
<summary>🤝 <strong>Collaborative AI Querying</strong></summary>

- **Parallel model execution** - Query multiple models simultaneously
- **Named model sets** - Pre-configured groups for specific tasks (think, code, docs)
- **Custom suffixes** - Add context to guide model responses
- **Fresh mode** - Exclude conversation history for unbiased responses
- **Graceful failure handling** - If one model fails, others still respond
- **Response aggregation** - See all model outputs in one organized view

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

### Shortcuts Management
```bash
antomix shortcuts                                  # List all shortcuts
antomix shortcuts list                             # List all shortcuts
antomix shortcuts edit                             # Edit shortcuts file in nano
antomix shortcuts add <name> <profile/model>      # Add new shortcut
antomix shortcuts remove <name>                   # Remove shortcut  
antomix shortcuts stats                            # Show shortcuts statistics
```

### Collaborative AI Management
```bash
antomix colab                                      # List all colab sets
antomix colab list                                 # List all colab sets
antomix colab add <name> <models> [-- <suffix>]   # Add new colab set
antomix colab remove <name>                       # Remove colab set
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
<summary>💬 <strong>`$$` Runtime Commands</strong></summary>

Use these commands directly in Claude Code or any connected application:

### `$$set` Command - Temporary Model Switching
```bash
# Using shortcuts (fastest way)
$$set:gqw How does photosynthesis work?
$$set:o3pro Solve this complex reasoning task
$$set:grok4 Tell me a joke about programming

# Using full profile/model syntax  
$$set:groq/qwen/qwen3-32b Quick question here
$$set:openai/o3-pro Complex analysis needed
$$set:openrouter-qwen/x-ai/grok-4 Creative writing task
```

### Shortcuts Management
```bash
$$shortcuts                    # List all available shortcuts
$$shortcuts add myfast groq/llama-3.3-70b-versatile  # Add custom shortcut
$$shortcuts remove myfast      # Remove shortcut
$$shortcuts stats              # Show shortcuts statistics
```

### `$$colab` Command - Collaborative AI Queries
```bash
# Using named sets (recommended for common tasks)
$$colab think How do I scale this architecture to 1M users?
$$colab code Implement a rate limiter with Redis
$$colab docs Write API documentation for this endpoint

# Direct model lists (comma-separated, NO spaces!)
$$colab o3,gpt41,sonnet4 Analyze this code for security issues
$$colab gll,gdp,oqw fresh Compare these database options
$$colab oqwt,o3pro,grok4 What's wrong with this algorithm?

# Managing collaborative sets
$$colab set review gpt41,ogmf -- Please review this critically
$$colab set debug o3,gpt41 -- Debug this step by step
$$colab remove debug
$$colab                        # List all available sets
```

**Syntax:**
- `$$colab <set-name> <query>` - Use a pre-configured set
- `$$colab <models> [fresh] <query>` - Direct model list
- `$$colab set <name> <models> [-- <suffix>]` - Create new set
- `$$colab remove <name>` - Remove a set

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

## 🔑 How to Get API Keys

Don't have API keys yet? Here's where to create them:

### Free/Fast Providers
- **🔥 Groq** (Lightning fast inference) → [Get API Key](https://console.groq.com/keys)
- **🌟 OpenRouter** (100+ models, some free) → [Get API Key](https://openrouter.ai/keys)

### Premium Providers  
- **🤖 OpenAI** (GPT models) → [Get API Key](https://platform.openai.com/api-keys)
- **🧠 Anthropic** (Claude models) → [Get API Key](https://console.anthropic.com/keys)
- **💎 Google Gemini** → [Get API Key](https://aistudio.google.com/app/apikey)

### Specialty Providers
- **🔬 Mistral AI** → [Get API Key](https://console.mistral.ai/api-keys/)
- **🚀 xAI** (Grok models) → [Get API Key](https://console.x.ai/)

> [!TIP]
> **Start with Groq or OpenRouter!** They offer free tiers and are super fast. You can always add other providers later.

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

Following options will be available soon:

3. 💡 **Suggest features** via discussions
4. 🔀 **Submit PRs** for improvements

---

## 📄 License

License to be determined. Please check back for updates on licensing terms.

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