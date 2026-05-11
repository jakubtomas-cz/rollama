# rollama

Restart Ollama to free up resources.

**macOS only** — uses `launchctl` to manage the Ollama LaunchAgent.

## Usage

```bash
chmod +x rollama
./rollama
```

## Make it available globally

To run `rollama` from anywhere, add the directory containing the script to your `PATH`. 

For example, if you have the project in `~/path/to/rollama`, add a line like this to your shell configuration file (e.g., `~/.zshrc` or `~/.bash_profile`):

```bash
export PATH="$HOME/path/to/rollama:$PATH"
```

Then, restart your terminal or run `source ~/.zshrc` (or your respective config file).

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
