<h1 align="center">Disciplined Vibe Coding</h1>

<p align="center">
  One command for a fully local vibe-coding stack: <b>editor + Ollama + opencode</b>, wired together.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/macOS-000000?style=flat&logo=apple&logoColor=white" alt="macOS">
  <img src="https://img.shields.io/badge/Linux-FCC624?style=flat&logo=linux&logoColor=black" alt="Linux">
  <img src="https://img.shields.io/badge/Windows-0078D6?style=flat&logo=windows&logoColor=white" alt="Windows">
  <img src="https://img.shields.io/badge/100%25-local-2ea44f?style=flat" alt="100% local">
  <img src="https://img.shields.io/badge/no-API%20keys-blue?style=flat" alt="no API keys">
  <img src="https://img.shields.io/badge/model-qwen3%3A1.7b-orange?style=flat" alt="qwen3:1.7b">
</p>

No Docker (Ollama runs natively so the model can use your GPU), no cloud, no API keys.
The script installs everything; everything you build in the seminar you vibe yourself.

## 🚀 Quick start

You need `git` and a browser. Re-running the script is always safe.

**macOS / Linux**

```bash
git clone https://github.com/Quillstacks/disciplinedvibe.git
cd disciplinedvibe
bash bootstrap.sh
```

**Windows (PowerShell)**

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

Type what you want to build and press Enter. opencode writes **real files** into this
folder; you open and run them yourself.

<details>
<summary>🐣 <b>Never used a terminal? Start here</b></summary>

<br>

A terminal is just a text window where you type a command, press **Enter**, and wait
for it to finish. You do not need to understand the commands: copy, paste, run them one
line at a time, and keep the same window open for the whole seminar.

| System | Open a terminal | Paste |
|---|---|---|
| macOS | **Cmd + Space**, type `Terminal`, Enter | **Cmd + V** |
| Windows | **Windows key**, type `PowerShell`, Enter | **Ctrl + V** (or right-click) |
| Ubuntu / Linux | **Ctrl + Alt + T** | **Ctrl + Shift + V** (or right-click) |

**How to run a command:** click into the window, paste one line, press **Enter**, and
wait until the text stops scrolling before pasting the next.

On macOS the first `git` command may pop up *"Install the command line developer
tools"* — click **Install**, wait for it to finish, then carry on.

</details>

## 📦 What gets installed

| Component | macOS | Linux | Windows |
|---|---|---|---|
| Editor   | brew (micro / zed / vscode)            | apt/dnf/pacman / installer                    | winget                                     |
| Ollama   | Homebrew + `brew services` (autostart) | official installer + `systemctl enable --now` | winget / installer (autostart via Run key) |
| Model    | `qwen3:1.7b` (~1.4 GB, reasoning)      | same                                          | same                                       |
| opencode | official install script                | official install script                       | winget                                     |
| Config   | `~/.config/opencode/opencode.json` pointing at `http://localhost:11434/v1`                                                    |

## 🎛️ Knobs

**Editor** — default `micro`, a ~10 MB terminal editor (Ctrl-S saves, Ctrl-Q quits):

```bash
EDITOR=micro   bash bootstrap.sh   # default, lightweight, terminal
EDITOR=zed     bash bootstrap.sh   # native GUI, fast
EDITOR=vscode  bash bootstrap.sh   # extensions / Copilot-style UI
EDITOR=none    bash bootstrap.sh   # bare terminal, opencode renders its own diffs
```

**Model** — default `qwen3:1.7b`, a small reasoning model that reliably writes files.
Sharper models cost more RAM and a longer download:

```bash
MODEL=qwen3:4b bash bootstrap.sh   # 8 GB+ RAM, sharper, still builds reliably
MODEL=qwen3:8b bash bootstrap.sh   # 16 GB RAM, most reliable builds
MODEL=qwen2.5-coder:0.5b bash bootstrap.sh   # last resort for weak hardware; often will not write files
```

On Windows use `$env:EDITOR="zed";` / `$env:MODEL="qwen3:4b";` before the command.

## ✅ Verify it works

```bash
ollama run qwen3:1.7b "write an index.html with a button that shows an alert"   # model answers locally
opencode                                                                        # agent starts, talks to Ollama
```

## 🔧 Troubleshooting

<details>
<summary><b>opencode is not using your local model</b> (cloud model in the status bar, or <code>missing field name</code>)</summary>

<br>

Run `/models` and pick **Ollama (local)**. To make it stick,
`~/.config/opencode/opencode.json` needs `"model": "ollama/qwen3:1.7b"` near the top;
add that line yourself, or delete the file and rerun `bootstrap.sh`.

</details>

<details>
<summary><b><code>git: command not found</code> / <code>git is not recognized</code></b></summary>

<br>

git is not installed yet. macOS: rerun the `git clone` line and click **Install** on the
popup. Windows: install it from [git-scm.com](https://git-scm.com/download/win), then
open a fresh PowerShell window. Ubuntu: `sudo apt-get install -y git`.

</details>

<details>
<summary><b><code>ollama</code> command not found after install (Windows)</b></summary>

<br>

Open a fresh PowerShell window — the installer updates `PATH` for new shells only.

</details>

<details>
<summary><b>Port 11434 already in use</b></summary>

<br>

Another Ollama is running. `pkill ollama` (Unix) / Task Manager (Windows), then rerun.

</details>

<details>
<summary><b>Model download is slow, or Linux has no systemd, or you are behind a proxy</b></summary>

<br>

- **Slow download:** `qwen3:1.7b` is ~1.4 GB; the sub-1 GB `MODEL=qwen2.5-coder:0.5b`
  downloads faster but often will not write files.
- **Linux without systemd / snap:** the script falls back to `nohup ollama serve &`;
  add it to your shell rc for persistence.
- **Corporate proxy:** set `HTTPS_PROXY` before running. Ollama also reads `OLLAMA_HOST`.

</details>

## 🧹 Uninstall

<details>
<summary>Remove Ollama, the model, and config</summary>

<br>

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

</details>
