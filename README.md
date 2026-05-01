# ollama-restart

Restart Ollama to free up resources.

**macOS only** — uses `launchctl` to manage the Ollama LaunchAgent.

## Usage

```bash
chmod +x ollama-restart.sh
./ollama-restart.sh
```

## What it does

1. Kills all running Ollama processes
2. Waits briefly for ports to free
3. Restarts Ollama via macOS LaunchAgent

## Note

The LaunchAgent runs in its own environment, so **environment variables** (e.g. `OLLAMA_HOST`, `OLLAMA_MODELS`, `OLLAMA_KEEP_ALIVE`) set in your shell **will not be picked up** after restart.

To set env vars, add `launchctl setenv` lines directly to the script before the `launchctl start` call:

```bash
launchctl setenv OLLAMA_HOST "0.0.0.0:11434"
launchctl setenv OLLAMA_MODELS "/Volumes/Models/ollama"
launchctl setenv OLLAMA_KEEP_ALIVE "24h"
```
