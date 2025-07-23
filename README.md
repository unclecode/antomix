# Antomix

Bidirectional proxy between Anthropic and OpenAI APIs.

## Installation

```bash
npm install -g antomix
```

## Usage

### CLI Commands

```bash
# Start the proxy server
antomix start --port 3000

# Stop the proxy server
antomix stop

# Check status
antomix status

# View usage statistics
antomix usage

# View logs
antomix logs -f
```

### Proxy Modes

The proxy supports both directions simultaneously:

- **Anthropic → OpenAI**: Send Anthropic-formatted requests to `/v1/messages`
- **OpenAI → Anthropic**: Send OpenAI-formatted requests to `/v1/chat/completions`

### Dynamic Configuration

You can override model mappings via query parameters:

```bash
curl -X POST "http://localhost:3000/v1/messages?map={\"claude-opus-4\":\"gpt-4\"}"
```

## License

MIT

## Support

For issues and feature requests, please visit our [GitHub repository](https://github.com/yourusername/antomix).
