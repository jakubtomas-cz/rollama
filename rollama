#!/bin/bash
# Restart Ollama to free up resources

set -e

echo "Stopping Ollama..."

# Kill all Ollama processes
killall Ollama 2>/dev/null || true
killall ollama 2>/dev/null || true

# Wait for processes to fully exit and ports to free
sleep 2

echo "Starting Ollama..."

# Restart via LaunchAgent
launchctl stop com.ollama.ollama 2>/dev/null || true
launchctl setenv OLLAMA_KEEP_ALIVE "10m"
launchctl start com.ollama.ollama

echo "Ollama restarted successfully."
