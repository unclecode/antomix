# 🚀 Antomix - Universal **Claude Code** Proxy | Bidirectional Anthropic ↔ OpenAI API Bridge

[![npm version](https://img.shields.io/npm/v/antomix.svg)](https://www.npmjs.com/package/antomix)
[![License: TBD](https://img.shields.io/badge/License-TBD-orange.svg)](#)
[![Node.js Version](https://img.shields.io/badge/node-%3E%3D16.0.0-brightgreen)](https://nodejs.org/)

> **Use Claude Code with ANY AI model** - OpenAI, Groq, Gemini, Local Models, OpenRouter's 100+ models, and more!

https://github.com/user-attachments/assets/5fdfce3d-dc20-4825-b4df-ea2787e54858

## 🎯 Why Antomix?

**Hey there! I'm [Unclecode](https://github.com/unclecode), author of [Crawl4AI](https://github.com/unclecode/crawl4ai) (![GitHub Repo stars](https://img.shields.io/github/stars/unclecode/crawl4ai?style=social) ⭐).** 

After trying alternatives like Gemini CLI and Qwen Code, I realized something: **The magic of Claude Code isn't just the model - it's the assistant itself.** The way it's engineered as an agentic coding assistant is what makes it so efficient. I wanted this incredible experience with **ALL models**, not just Claude. So I built Antomix!

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
# Local models (Ollama) work without API keys!
```

### 3️⃣ Launch Claude Code with Any Model
```bash
# Interactive selection - choose with arrow keys ✅/❌ indicators
antomix claude

# Or specify profile directly  
antomix claude --profile openrouter-qwen # [openai|groq|gemini|ollama|...]
```

> **💡 Tip:** Use `antomix profiles` to list all available profiles. Missing API keys? Antomix guides you through setup!

> [!IMPORTANT]
> **When you exit Claude Code, the proxy automatically stops and cleans up!**

*[GIF Here I will add a video or GIF animation to show how it works]*

### 3️⃣ Collaborative AI - Query Multiple Models Simultaneously

**Get diverse perspectives from multiple AI models in one shot!** The `$$colab` command lets you query several models in parallel and see all their responses together.

```bash
# Ask multiple models for help debugging
$$colab o3,gpt41,groq-qwen,grok4 Why is my Redis connection timing out in production?

# Get creative ideas from different AI perspectives  
$$colab gpt41,open-geminipro,sonnet4,grok4 Write a catchy marketing tagline for an eco-friendly water bottle

# Compare solutions from various models
$$colab o3,open-qwen,groq-deepseek,groq-llama What is the most efficient sorting algorithm for partially sorted data

# Use `fresh` to exclude conversation history for unbiased responses
$$colab open-qwen,o3pro,sonnet4 fresh Review this architecture without context
```

**How it works:**
- List models separated by commas (NO spaces: `o3,gpt41,groq-llama` ✅ not `o3, gpt41, groq-llama` ❌)
- Models execute in parallel - if one fails, others still respond
- See all responses in one organized view

> [!TIP]
> Check the detailed docs below for pre-configured model sets like `think`, `code`, and `docs` that group the best models for specific tasks!

https://github.com/user-attachments/assets/1a48f6e0-1f4c-408d-b100-88f26bb4e343

### 4️⃣ `$$` Command - Use Any Model for Single Messages

Switch models temporarily for individual messages without changing your main profile:

```bash
# Using shortcuts (25+ pre-configured) - just type $$[shortcut]
$$groq-qwen What is the capital of France?
$$o3pro Solve this complex problem: [problem]  
$$open-grok4 Write a funny story about AI
$$groq-llama Fast Groq inference

# Or use explicit $$set: syntax
$$set:groq-qwen What is the capital of France?
$$set:o3pro Solve this complex problem: [problem]

# Using direct profile/model syntax with $$set:
$$set:groq/llama-3.3-70b-versatile Explain quantum computing
$$set:openai/o3-pro Analyze this code: [code]
$$set:openrouter-qwen/anthropic/claude-opus-4 Deep analysis needed
```

**Available shortcuts:**
- **Groq**: `groq-qwen` `groq-llama` `groq-deepseek` `groq-kimi2` (fast inference)
- **OpenAI**: `o3pro` `o3` `o3mini` `o4` `gpt41` (latest models) 
- **OpenRouter**: `open-qwen` `open-geminipro` `open-mistral` `open-grok4` (100+ models)
- **Anthropic**: `opus4` `sonnet4` `haiku35` (Claude models via OpenRouter)

> [!TIP]
> **Create your own shortcuts!** Add custom shortcuts in `~/.antomix/shortcuts.yml` or use `antomix shortcuts add mymodel profile/model`. See [Shortcuts Management](#shortcuts-management) below for details.

Manage profiles and system settings:

```bash
$$switch-profile groq          # Switch main profile to Groq
$$status                       # Check current model and status
$$shortcuts                    # List and manage shortcuts  
$$profiles                     # See all available profiles
```

> [!TIP]
> **`$$[shortcut]` is the easiest way!** Just type `$$groq-qwen message` instead of `$$set:groq-qwen message`. Both work!
> **Temporary vs Permanent:** `$$` commands are temporary (one message), `$$switch-profile` is permanent (changes your main model).

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
<summary>🔄 <strong>Proxy Mode Control</strong></summary>

Control whether the proxy converts requests or passes them through directly:

```bash
# Enable proxy conversion (default)
$$proxy on
# → Converts Claude requests to target model requests
# → Uses the current profile's model mappings
# → This is the normal operating mode

# Disable proxy conversion (passthrough)
$$proxy off  
# → Direct passthrough to original APIs
# → No conversion or modification
# → Useful for debugging or using original APIs

# Check current proxy status
$$proxy status
# → Shows if proxy is ON (converting) or OFF (passthrough)
```

The `$$status` command also shows proxy status alongside profile info.

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
- **Proxy mode** for direct API access

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
antomix profiles                                   # List all available profiles
antomix profiles list                             # List all available profiles
antomix profiles list --verbose                   # Show detailed profile information
antomix profiles show groq                        # Show full YAML configuration of a profile
antomix profiles create                           # Create a new custom profile interactively
antomix profiles create my-provider              # Create profile with specific name
antomix profiles create groq                      # Duplicate existing 'groq' profile
antomix profiles edit my-provider                # Edit custom profile in nano
antomix profiles remove my-provider              # Remove custom profile
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

### AI Help Assistant

Get instant help and answers about Antomix using AI:

```bash
antomix ask "<question>"                           # Ask questions about Antomix
antomix ask "how do I create a custom profile?"    # Get help with specific tasks
antomix ask "what models are available?"           # Learn about available models
antomix ask "how to use $$colab command?"          # Learn about specific features
```

**Features:**
- 🤖 Uses AI to answer questions based on the official README documentation
- 📚 Automatically fetches latest docs from GitHub (24-hour cache)
- 🎨 Beautiful markdown-formatted responses in your terminal
- 🔄 Remembers your preferred AI profile for consistent experience
- ⚡ Streaming responses with animated spinner

**First-time setup:**
- Select your preferred AI profile on first use
- Change profile anytime: `rm ~/.antomix/cache/ask-profile.json`

**Note:** Quotes are required for questions with special characters:
```bash
antomix ask "how to create a profile?"    # ✅ Correct
antomix ask how to create a profile?      # ❌ Shell may interpret ? as wildcard
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

### `$$` Command - Temporary Model Switching
```bash
# Using shortcuts (fastest way) - just type $$[shortcut]
$$groq-qwen How does photosynthesis work?
$$o3pro Solve this complex reasoning task
$$open-grok4 Tell me a joke about programming

# Or use explicit $$set: syntax
$$set:groq-qwen How does photosynthesis work?
$$set:o3pro Solve this complex reasoning task

# Using full profile/model syntax with $$set:
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

**Creating Custom Shortcuts:**
- Edit `~/.antomix/shortcuts.yml` directly
- Or use CLI: `antomix shortcuts add mymodel profile/model`
- Example: `antomix shortcuts add mychat openai/gpt-4`
- Then use it: `$$mychat What is the weather like?`

### `$$colab` Command - Collaborative AI Queries
```bash
# Using named sets (recommended for common tasks)
$$colab think How do I scale this architecture to 1M users?
$$colab code Implement a rate limiter with Redis
$$colab docs Write API documentation for this endpoint

# Direct model lists (comma-separated, NO spaces!)
$$colab o3,gpt41,sonnet4 Analyze this code for security issues
$$colab groq-llama,groq-deepseek,open-qwen fresh Compare these database options
$$colab open-qwen,o3pro,grok4 What is wrong with this algorithm?

# Managing collaborative sets
$$colab set review gpt41,open-geminiflash -- Please review this critically
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
$$proxy on                    # Enable proxy conversion (Claude → Target models)
$$proxy off                   # Disable proxy (direct passthrough mode)
$$proxy status                # Check if proxy is converting or passthrough
$$ping                        # Test connectivity
$$help                        # Show all $ commands
$$export <filename>           # Export current config
$$ask <question>              # Get AI-powered help using current profile
```

**$$ask Command:**
- Uses your current profile's AI model to answer questions about Antomix
- Reads from the cached README documentation 
- Works inside Claude Code or any connected app
- Example: `$$ask how do I create a custom profile?`
- Note: Requires running `antomix ask` from CLI first to cache docs

</details>

---

## 🔧 Creating Custom Profiles

<details>
<summary>🆕 <strong>Interactive Profile Creation</strong></summary>

Create custom profiles easily with the interactive CLI:

```bash
# Create a new profile interactively
antomix profiles create

# Create with a specific name
antomix profiles create my-provider
```

The interactive wizard will guide you through:
- 🏷️ Profile name and description
- 🌐 API base URL configuration
- 🔑 Environment variable for API key
- 🤖 Model mappings (Claude → Your provider)
- 🔧 Parameter transformations
- 📦 Custom headers (optional)

**Example session:**
```bash
$ antomix profiles create

🔧 Create New Profile
Press Enter to use default values

Profile filename: my-llm
Display name: My LLM Provider
Description: Custom LLM provider for specialized models
API base URL: https://api.myllm.com/v1
Environment variable for API key: MY_LLM_API_KEY
Add custom headers? No

Model Mappings (map Claude models to your provider's models):
Map claude-opus-4 to: my-llm-large
Map claude-sonnet-4 to: my-llm-medium
Map claude-3-5-haiku to: my-llm-fast

✅ Profile created successfully!
   Location: ~/.antomix/profiles/my-llm.yml
   Environment variable: MY_LLM_API_KEY

To use this profile:
  1. Set your API key: export MY_LLM_API_KEY="your-api-key"
  2. Start with: antomix claude --profile my-llm
  3. Or switch to it: $$switch-profile my-llm
```

</details>

<details>
<summary>📝 <strong>Profile YAML Structure</strong></summary>

Custom profiles are stored in `~/.antomix/profiles/` as YAML files:

```yaml
# ~/.antomix/profiles/my-custom.yml
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
    Authorization: "Bearer $YOUR_PROVIDER_API_KEY"
```

You can manually edit these files after creation to fine-tune settings.

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