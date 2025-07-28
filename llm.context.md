# Antomix LLM Context - Complete Knowledge Base

This document serves as a comprehensive knowledge base for AI assistants to understand and help users with Antomix. It contains detailed technical information, implementation details, and usage patterns.

## Table of Contents
1. [System Overview](#system-overview)
2. [Architecture](#architecture)
3. [Installation & Setup](#installation--setup)
4. [Command Reference](#command-reference)
5. [Profile System](#profile-system)
6. [Model Mapping](#model-mapping)
7. [API Translation](#api-translation)
8. [Configuration Files](#configuration-files)
9. [Runtime Commands](#runtime-commands)
10. [Collaborative AI](#collaborative-ai)
11. [Troubleshooting](#troubleshooting)
12. [Implementation Details](#implementation-details)
13. [Best Practices](#best-practices)

---

## System Overview

### What is Antomix?
Antomix is a universal proxy that allows Claude Code (and any Anthropic API client) to work with ANY AI model provider. It acts as a bidirectional bridge between Anthropic's API format and other providers like OpenAI, Groq, Gemini, Ollama, and OpenRouter.

### Core Purpose
- Enable Claude Code to work with 100+ different AI models
- Seamless API translation between Anthropic ↔ OpenAI formats
- Hot-swapping models without restarting applications
- Support for local models via Ollama
- Collaborative AI queries across multiple models

### Key Components
1. **Proxy Server** (`server.js`) - Main HTTP proxy handling requests
2. **CLI Tool** (`cli.js`) - Command-line interface for management
3. **Converters** - Bidirectional API format translation
4. **Profile System** - Model and provider configurations
5. **Command System** - Runtime control via $$ commands
6. **Shortcut Manager** - Quick model switching shortcuts

---

## Architecture

### Request Flow
1. Client (e.g., Claude Code) sends Anthropic API request to proxy
2. Proxy intercepts request on configured port (default: 3000)
3. Request analyzer determines if it contains $$ commands
4. Converter translates Anthropic format to target provider format
5. Request forwarded to actual AI provider
6. Response converted back to Anthropic format
7. Client receives response as if from Anthropic

### Core Files
- `server.js` - Express server implementing the proxy
- `cli.js` - CLI implementation with all commands
- `commands.js` - $$ command handlers
- `profile-loader.js` - Profile management system
- `shortcuts.js` - Shortcut and colab set management
- `converters/anthropic-to-openai.js` - Format converter
- `converters/openai-to-anthropic.js` - Reverse converter
- `converters/colab-reducer.js` - Multi-model response aggregation
- `usage-tracker.js` - Token usage and analytics

### Directory Structure
```
~/.antomix/
├── profiles/          # Custom user profiles
├── logs/             # Daily and session logs
│   ├── daily/
│   └── sessions/
├── cache/            # Cached data
│   ├── README.md     # Documentation cache
│   └── ask-profile.json
├── exports/          # Exported configurations
└── shortcuts.yml     # User-defined shortcuts
```

---

## Installation & Setup

### Installation Methods
1. **Global NPM Install**: `npm install -g antomix`
2. **Local Development**: Clone repo and `npm link`

### Initial Setup
1. Set environment variables for API keys
2. Choose a profile when launching
3. Configure ANTHROPIC_BASE_URL for service mode

### Environment Variables
- `GROQ_API_KEY` - Groq API access
- `OPENAI_API_KEY` - OpenAI API access
- `GEMINI_API_KEY` - Google Gemini access
- `OPENROUTER_API_KEY` - OpenRouter access
- `ANTHROPIC_BASE_URL` - Points apps to proxy
- `PORT` - Proxy server port (default: 3000)

---

## Command Reference

### CLI Commands

#### Service Management
- `antomix start [--profile <name>] [--port <port>]` - Start proxy server
- `antomix stop` - Stop running server
- `antomix status` - Show server status
- `antomix switch <profile>` - Switch profile on running server

#### Claude Integration
- `antomix claude [--profile <name>]` - Launch Claude Code with proxy
- Interactive profile selection with ✅/❌ indicators
- Auto-cleanup when Claude Code exits

#### Profile Management
- `antomix profiles [list] [--verbose]` - List all profiles
- `antomix profiles show <name>` - Show profile YAML
- `antomix profiles create [name]` - Interactive profile creation
- `antomix profiles edit <name>` - Edit custom profile
- `antomix profiles remove <name>` - Delete custom profile

#### Shortcut Management
- `antomix shortcuts [list]` - List all shortcuts
- `antomix shortcuts add <name> <profile/model>` - Add shortcut
- `antomix shortcuts remove <name>` - Remove shortcut
- `antomix shortcuts edit` - Edit shortcuts file
- `antomix shortcuts stats` - Show statistics

#### Collaborative AI
- `antomix colab [list]` - List colab sets
- `antomix colab add <name> <models> [-- <suffix>]` - Add set
- `antomix colab remove <name>` - Remove set

#### Logs and Monitoring
- `antomix logs [--follow] [--level <level>] [--session <id>]`
- Log levels: error, warn, info
- Session-specific filtering

#### AI Help Assistant
- `antomix ask "<question>"` - Get AI-powered help
- Fetches latest docs from GitHub
- Uses selected AI profile
- Markdown-formatted responses

#### Utilities
- `antomix export <filename>` - Export configuration
- `antomix --help` - Show help
- `antomix --version` - Show version

---

## Profile System

### Profile Structure
Profiles are YAML files defining how to connect to AI providers:

```yaml
name: "Provider Name"
description: "Description of the provider"

# Model mappings - Claude model -> Provider model
models:
  "claude-opus-4-20250514": 
    - "provider-best-model"
  "claude-sonnet-4-20250514": 
    - "provider-balanced-model"
  "claude-3-5-haiku-20241022": 
    - "provider-fast-model"

# Parameter transformations
parameters:
  "*":  # Apply to all models
    "[max_tokens]": "max_completion_tokens"
    "max_completion_tokens": 16000

# API configuration
api:
  base_url: "https://api.provider.com/v1"
  api_key: "$PROVIDER_API_KEY"
  headers:
    Authorization: "Bearer $PROVIDER_API_KEY"
```

### Built-in Profiles
1. **groq** - Lightning-fast inference
2. **openai** - GPT models including o3
3. **gemini** - Google's models
4. **ollama** - Local models
5. **openrouter-** variants - 100+ models
6. **default** - OpenAI with specific mappings

### Custom Profiles
- Stored in `~/.antomix/profiles/`
- Override built-in profiles
- Support environment variables
- Custom headers and parameters

---

## Model Mapping

### Mapping System
Maps Anthropic model names to provider-specific models:
- `claude-opus-4-20250514` → Target provider's best model
- `claude-sonnet-4-20250514` → Target provider's balanced model
- `claude-3-5-haiku-20241022` → Target provider's fast model

### Dynamic Mapping
- Runtime override: `$$map <model> <target>`
- Temporary override: `$$set:profile/model`
- Profile-based persistent mapping

### Converted Models Cache
Profile loader creates `convertedModels` with bidirectional mappings:
- `ant_to_oai`: Anthropic → Provider
- `oai_to_ant`: Provider → Anthropic

---

## API Translation

### Anthropic to OpenAI
Handles conversion of:
- Message format (single content → array)
- System messages (first user message)
- Max tokens parameter
- Streaming response format
- Tool calls and function calling
- Temperature and other parameters

### OpenAI to Anthropic
Reverse conversion for:
- Response format
- Usage statistics
- Stream chunks
- Error responses
- Tool call results

### Special Handling
- Multimodal content (images)
- Token counting
- Stop sequences
- Response formatting

---

## Configuration Files

### shortcuts.yml
```yaml
shortcuts:
  groq-qwen: "groq/qwen/qwen-2.5-coder-32b-instruct"
  o3pro: "openai/o3-pro"
  
colab_sets:
  think:
    models: "o3,gpt41,sonnet4"
    suffix: "Think step by step"
```

### Profile YAML Files
Located in:
- Built-in: `/config/profiles/`
- Custom: `~/.antomix/profiles/`

### Cache Files
- `~/.antomix/cache/README.md` - Documentation cache
- `~/.antomix/cache/ask-profile.json` - AI assistant profile

---

## Runtime Commands

### Profile & Status Commands
- `$$status` - Current profile and model mappings
- `$$switch-profile <name>` - Change active profile
- `$$profiles` - List available profiles
- `$$cat-profile <name>` - Show profile configuration

### Model Commands
- `$$models` - Show current model mappings
- `$$map <model> <target>` - Override model mapping
- `$$set:<shortcut> <message>` - Use specific model for one message
- `$$set:profile/model <message>` - Direct model specification

### Proxy Control
- `$$proxy on` - Enable proxy conversion
- `$$proxy off` - Passthrough mode
- `$$proxy status` - Check proxy state

### Collaborative AI
- `$$colab <models> <query>` - Query multiple models
- `$$colab <set-name> <query>` - Use predefined set
- `$$colab set <name> <models> [-- <suffix>]` - Create set
- `$$colab remove <name>` - Delete set

### Utilities
- `$$ping` - Test connectivity
- `$$help` - Show all commands
- `$$export <filename>` - Export configuration
- `$$ask <question>` - Get AI help about Antomix
- `$$shortcuts` - Manage shortcuts

---

## Collaborative AI

### Overview
Query multiple AI models simultaneously for diverse perspectives.

### Usage Patterns
1. **Direct model list**: `$$colab o3,gpt41,sonnet4 <query>`
2. **Named sets**: `$$colab think <query>`
3. **Fresh queries**: `$$colab models fresh <query>`

### Model Sets
Predefined sets for common tasks:
- `think` - Best reasoning models
- `code` - Top coding models
- `docs` - Documentation specialists

### Response Aggregation
- Parallel execution
- Individual model responses
- Formatted output with model labels
- Error handling per model

---

## Troubleshooting

### Common Issues

#### API Key Problems
- **Symptom**: "API key not found" errors
- **Solution**: Set environment variable, check spelling
- **Debug**: `echo $API_KEY_NAME`

#### Profile Not Found
- **Symptom**: "Profile 'x' not found"
- **Solution**: Check `antomix profiles list`
- **Debug**: Check `~/.antomix/profiles/`

#### Connection Errors
- **Symptom**: "ECONNREFUSED" errors
- **Solution**: Check if proxy is running with `antomix status`
- **Debug**: Check port availability

#### Model Mapping Issues
- **Symptom**: "Model not supported"
- **Solution**: Check profile's model mappings
- **Debug**: Use `$$models` command

### Debug Commands
- `antomix logs --level error` - See error logs
- `antomix logs --follow` - Real-time log monitoring
- `$$status` - Check current configuration
- `$$ping` - Test basic connectivity

### Log Locations
- Daily logs: `~/.antomix/logs/daily/`
- Session logs: `~/.antomix/logs/sessions/`
- Error logs: Separate error log files

---

## Implementation Details

### Proxy Server
- Built with Express.js
- Middleware for logging and command detection
- Request/response interceptors
- WebSocket support for streaming

### Command Detection
- Regex pattern: `/\$\$[a-zA-Z][a-zA-Z0-9-]*/`
- Extracted from message content
- Processed before API forwarding
- Response injection for command results

### Profile Loading
- Searches multiple directories
- User profiles override built-in
- Dynamic reload capability
- Validation on load

### Token Tracking
- Per-session usage tracking
- Model-specific token counting
- Cost calculation
- Usage statistics export

### Error Handling
- Graceful degradation
- Detailed error messages
- Fallback mechanisms
- Recovery strategies

---

## Best Practices

### Profile Creation
1. Use environment variables for API keys
2. Map all Claude models for compatibility
3. Set reasonable token limits
4. Test with `$$ping` after creation

### Model Selection
1. Match use case to model strengths
2. Consider cost vs performance
3. Use shortcuts for frequent models
4. Test with `$$set` before switching

### Performance Optimization
1. Use Groq for fast responses
2. Local models for privacy
3. Batch requests when possible
4. Monitor token usage

### Security
1. Never commit API keys
2. Use environment variables
3. Restrict proxy access
4. Review exported configs

### Debugging
1. Start with `--verbose` flag
2. Check logs for details
3. Test with `$$ping`
4. Verify with `$$status`

---

## Advanced Features

### Custom Headers
Add provider-specific headers in profiles:
```yaml
api:
  headers:
    X-Custom-Header: "value"
    Authorization: "Bearer $API_KEY"
```

### Parameter Transformations
Rename or set default parameters:
```yaml
parameters:
  "*":
    "[old_name]": "new_name"
    "fixed_param": 1000
```

### Multi-Model Fallbacks
Profiles can list multiple models for fallback:
```yaml
models:
  "claude-opus-4-20250514":
    - "primary-model"
    - "fallback-model"
```

### Streaming Optimizations
- Chunked transfer encoding
- Minimal buffering
- Real-time conversion

---

## Error Messages and Solutions

### "Profile 'X' not found"
- Available profiles: Use `antomix profiles list`
- Create custom: `antomix profiles create X`

### "API key not set"
- Set environment variable
- Or add directly to profile (less secure)

### "Model not supported"
- Check profile model mappings
- Use `$$map` to override
- Update profile configuration

### "Connection refused"
- Start proxy: `antomix start`
- Check port: Default is 3000
- Verify ANTHROPIC_BASE_URL

### "Invalid command"
- Use `$$help` for command list
- Check command syntax
- Verify spacing and arguments

---

## Version History

### Current Version: 1.3.0
- AI-powered help assistant
- Markdown rendering in terminal
- Enhanced profile management
- Improved error messages

### Recent Updates
- Proxy mode replacing bypass
- Collaborative AI queries
- Profile CRUD operations
- Shortcut management system

---

## Technical Specifications

### Supported Providers
- OpenAI (including o3 models)
- Anthropic (native passthrough)
- Google Gemini
- Groq
- Ollama (local)
- OpenRouter (100+ models)
- Any OpenAI-compatible API

### API Compatibility
- Anthropic Messages API
- OpenAI Chat Completions API
- Streaming responses
- Function calling
- Tool use
- Multimodal inputs

### Performance
- Minimal latency overhead
- Streaming preservation
- Efficient memory usage
- Concurrent request handling

---

This knowledge base is designed for AI assistants to provide accurate, detailed help about Antomix. Always refer to specific sections when answering user questions and provide exact commands or configuration examples when applicable.