# ask - AI CLI tool

A lightweight bash script for querying AI models via the Mistral API, optimized for direct, executable output.

This script is using free models, you can check the API pricing in https://mistral.ai/pricing#api-pricing.

You can create your API key at https://admin.mistral.ai/organization/api-keys.

## Quick start

### Option 1: One-line install with curl (recommended)

```bash
curl -sS https://raw.githubusercontent.com/GuilhermeGreggio/ask-mistral/main/install.sh | bash

# Set your Mistral API key
export MISTRAL_API_KEY="your-api-key-here"

# Test it
ask --test
```

### Option 2: Manual installation

```bash
# Clone and setup
git clone https://github.com/GuilhermeGreggio/ask-mistral.git
cd ask-mistral

chmod +x ask
sudo cp ask /usr/local/bin/

# Set your Mistral API key
export MISTRAL_API_KEY="your-api-key-here"

# Test it
ask --test
```

## Usage

### Basic usage

```bash
ask ffmpeg command to convert mp4 to gif
```

### Model selection

```bash
# Default model (Devstral Medium)
ask find files larger than 20mb

# Shorthand flags for quick model switching
ask -m "prompt"  # Devstral Medium (default)
ask -s "prompt"  # Devstral Small (faster)

# Custom model by full name
ask -m "devstral-medium-latest" "Explain this concept"
```


### System prompts

```bash
# Custom system prompt
ask --system "You are a pirate" "Tell me about sailing"

# Disable system prompt for raw model behavior
ask -r "What is 2+2?"
```

### Streaming mode

Get responses as they're generated:

```bash
ask --stream "Tell me a long story"
```

### Pipe input

```bash
echo "Fix this code: print('hello world)" | ask
cat script.py | ask "Review this code"
```

## Options

| Option | Description |
|--------|-------------|
| `-m` | Use Devstral Medium (default) |
| `-s` | Use Devstral Small (faster) |
| `-m MODEL` | Use custom model |
| `-r` | Disable system prompt |
| `--stream` | Enable streaming output |
| `--system` | Set custom system prompt |
| `-h, --help` | Show help message |

## Common use cases

### Command generation
```bash
# Get executable commands directly
ask "Command to find files larger than 100MB"
# Output: find . -type f -size +100M

ask "ffmpeg command to convert mp4 to gif"
# Output: ffmpeg -i input.mp4 -vf "fps=10,scale=320:-1:flags=lanczos" output.gif
```

### Code generation
```bash
# Generate code snippets
ask "Python function to calculate factorial"

# Code review
cat script.py | ask "Find potential bugs in this code"
```

### Quick answers
```bash
# Calculations
ask "What is 18% of 2450?"
# Output: 441

# Technical questions
ask "What port does PostgreSQL use?"
# Output: 5432
```

### Advanced usage
```bash
# Chain commands
ask "List all Python files" | ask "Generate a script to check syntax of these files"

# Use with other tools
docker ps -a | ask "Which containers are using the most memory?"

```

## Requirements

### Dependencies
- `bash` - Shell interpreter
- `curl` - HTTP requests to Mistral API
- `jq` - JSON parsing for API responses
- `bc` - Performance metrics calculation

### API access
- Mistral API key (get one at [console.mistral.ai](https://console.mistral.ai))
- Set as environment variable: `MISTRAL_API_KEY`

## License

MIT
