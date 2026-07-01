# Disciplined Vibe Coding — local LLM setup

One command gets you a fully local, offline-capable vibe-coding stack on your own
machine: an **editor + Ollama (local model, autostart) + opencode**, wired
together. No Docker (Ollama runs natively so the model can use your GPU), no cloud,
no API keys. Works on **macOS, Ubuntu/Linux, and Windows**.

That is all this repo does. Everything you build in the seminar you vibe yourself.

## Quick start

You need `git` and a browser. Everything else (editor, Ollama, a coding model,
opencode) is installed for you. Re-running the script is always safe.

### macOS / Linux

```bash
git clone https://github.com/Quillstacks/disciplinedvibe.git
cd disciplinedvibe
bash bootstrap.sh
```

### Windows (PowerShell)

```powershell
git clone https://github.com/Quillstacks/disciplinedvibe.git
cd disciplinedvibe
powershell -ExecutionPolicy Bypass -File bootstrap.ps1
```

When it finishes, you are ready to vibe in any folder:

```bash
mkdir -p ~/vibe && cd ~/vibe
opencode
```

## What gets installed

| Component | macOS | Linux | Windows |
|---|---|---|---|
| Editor   | brew (micro / zed / vscode)            | apt/dnf/pacman / installer                    | winget                                     |
| Ollama   | Homebrew + `brew services` (autostart) | official installer + `systemctl enable --now` | winget / installer (autostart via Run key) |
| Model    | `qwen2.5-coder:1.5b` (~1 GB)           | same                                          | same                                       |
| opencode | official install script                | official install script                       | winget                                     |
| Config   | `~/.config/opencode/opencode.json` pointing at `http://localhost:11434/v1`                                                    |

## Knobs

Pick a different editor (default is **`micro`**, a ~10 MB terminal editor: Ctrl-S
saves, Ctrl-Q quits, keeps the whole workbench in one terminal window):

```bash
EDITOR=micro   bash bootstrap.sh   # default, lightweight, terminal
EDITOR=zed     bash bootstrap.sh   # native GUI, fast
EDITOR=vscode  bash bootstrap.sh   # extensions / Copilot-style UI
EDITOR=none    bash bootstrap.sh   # bare terminal — opencode renders its own diffs
```

Pick a different model:

```bash
MODEL=qwen2.5-coder:7b   bash bootstrap.sh   # ~16 GB RAM, sharper
MODEL=qwen2.5-coder:0.5b bash bootstrap.sh   # weak hardware / slow link
```

On Windows use `$env:EDITOR="zed";` / `$env:MODEL="qwen2.5-coder:7b";` before the
command.

## Verify it works

```bash
ollama run qwen2.5-coder:1.5b "write a python fizzbuzz"   # model answers locally
opencode                                                  # agent starts, talks to Ollama
```

## Troubleshooting

- **`ollama` command not found after install (Windows):** open a fresh PowerShell
  window — the installer updates `PATH` for new shells only.
- **Port 11434 already in use:** another Ollama is running. `pkill ollama` (Unix) /
  Task Manager (Windows), then rerun.
- **Model download is slow:** the 1.5b model is ~1 GB; on a slow link switch to
  `MODEL=qwen2.5-coder:0.5b`.
- **Linux without systemd / snap:** the script falls back to `nohup ollama serve &`;
  add it to your shell rc for persistence.
- **Corporate proxy:** set `HTTPS_PROXY` before running. Ollama also reads
  `OLLAMA_HOST`.

## Uninstall

```bash
# macOS
brew services stop ollama && brew uninstall ollama
brew uninstall micro 2>/dev/null
rm -rf ~/.ollama ~/.config/opencode

# Linux
sudo systemctl disable --now ollama
sudo rm /etc/systemd/system/ollama.service /usr/local/bin/ollama
rm -rf ~/.ollama ~/.config/opencode
```
