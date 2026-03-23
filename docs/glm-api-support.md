# GLM API Support (智谱 AI 兼容)

This document describes how to use the Claude Code Discord Bot with GLM API (智谱 AI) instead of the official Anthropic API.

## Overview

The bot supports GLM API as a drop-in replacement for Anthropic API. This allows users in China to use the bot with lower latency and local compliance.

## Configuration

### Environment Variables

Add the following to your `.env` file:

```env
# GLM API Configuration
ANTHROPIC_BASE_URL=https://open.bigmodel.cn/api/anthropic
ANTHROPIC_AUTH_TOKEN=your_glm_api_token_here
ANTHROPIC_MODEL=glm-5
ANTHROPIC_DEFAULT_OPUS_MODEL=glm-5
ANTHROPIC_DEFAULT_SONNET_MODEL=glm-5
ANTHROPIC_DEFAULT_HAIKU_MODEL=glm-5

# Disable non-essential traffic
CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC=1
```

### Getting GLM API Token

1. Visit [智谱 AI Open Platform](https://open.bigmodel.cn/)
2. Create an account or log in
3. Generate an API token from the console
4. Use the token as `ANTHROPIC_AUTH_TOKEN`

## Features

### Direct Chat Mode

You can now send messages directly without using `/claude` command:

```
你好  → Bot responds automatically
```

### Claude Code Slash Commands

The following Claude Code slash commands are supported in chat:

| Command | Description |
|---------|-------------|
| `/compact` | Compact conversation history |
| `/cost` | Show token usage and cost |
| `/init` | Initialize project with CLAUDE.md |
| `/review` | Generate code review |
| `/security-review` | Generate security review |
| `/pr-comments` | Generate PR comments |
| `/release-notes` | Generate release notes |
| `/insights` | Show project insights |
| `/debug` | Enable debug mode |

### Simplified Output

By default, the bot hides verbose messages:
- "System: init" messages
- "Thinking" messages

To show all messages, set:
```env
DISCORD_VERBOSE=1
```

## Technical Details

### Environment Variable Filtering

The bot filters out potentially conflicting environment variables from the parent Claude Code process:

- `CLAUDE_CODE_ENTRYPOINT`
- `CLAUDECODE`
- `CLAUDE_CODE_SESSION_ID`
- `CLAUDE_CODE_IS_TTY`

These variables are removed before spawning the Claude Code subprocess to prevent SDK conflicts.

### Supported Models

| GLM Model | Equivalent |
|-----------|------------|
| `glm-5` | General purpose |
| `glm-4-plus` | High performance |
| `glm-4-air` | Fast responses |
| `glm-4-flash` | Ultra-fast |

## Troubleshooting

### Bot not responding

1. Check if the bot is in the correct channel
2. Verify your GLM API token is valid
3. Check the bot logs for errors

### "exited with code 1" error

This usually means:
- Invalid API token
- Network connectivity issues
- GLM API rate limiting

### Messages are slow

GLM API response times may vary. Consider:
- Using faster models like `glm-4-air` or `glm-4-flash`
- Reducing prompt complexity

## Migration from Anthropic API

To switch from Anthropic API to GLM API:

1. Update `.env` file with GLM configuration
2. Restart the bot
3. Test with a simple message

No code changes required!
