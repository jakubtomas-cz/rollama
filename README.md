# rollama

Restart Ollama to free up resources.

**macOS only** — uses `launchctl` to manage the Ollama LaunchAgent.

## Usage

```bash
chmod +x rollama.sh
./rollama.sh
```

## Make it available globally

To run `rollama` from anywhere, create a symlink:

```bash
sudo ln -s /path/to/rollama/rollama.sh /usr/local/bin/rollama
```

Then use it from any directory:

```bash
rollama
```

> **Gotcha:** After creating the symlink, open a **new shell** and wait a moment — the command may not be found immediately until the PATH is refreshed.

## What it does

1. Kills all running Ollama processes
2. Waits briefly for ports to free
3. Restarts Ollama via macOS LaunchAgent

## Note

The LaunchAgent runs in its own environment, so **environment variables** (e.g. `OLLAMA_HOST`, `OLLAMA_MODELS`, `OLLAMA_KEEP_ALIVE`) set in your shell **will not be picked up** after restart.

To set env vars, add `launchctl setenv` lines directly to the script before the `launchctl start` call:

```bash
launchctl setenv OLLAMA_HOST "0.0.0.0:11434"
launchctl setenv OLLAMA_KEEP_ALIVE "24h"
```
