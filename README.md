# Disciplined Vibe Coding — local LLM setup

One command gets you a fully local, offline-capable vibe-coding stack on your own
machine: an **editor + Ollama (local model, autostart) + opencode**, wired
together. No Docker (Ollama runs natively so the model can use your GPU), no cloud,
no API keys. Works on **macOS, Ubuntu/Linux, and Windows**.

That is all this repo does. Everything you build in the seminar you vibe yourself.

## Step 0 — Open a terminal (never coded before? start here)

Everything below happens in a **terminal**: a plain text window where you type a
command, press **Enter**, and wait for it to finish. You do not need to understand
the commands. Copy them, paste them, run them one line at a time. Keep this same
window open for the whole seminar.

**macOS**
1. Press **Cmd + Space** to open Spotlight (the search bar).
2. Type `Terminal` and press **Enter**. A window opens.
3. The first time you run a `git` command, macOS may pop up *"Install the command
   line developer tools"* — click **Install**, wait for it to finish, then carry on.

**Windows**
1. Press the **Windows key**.
2. Type `PowerShell` and press **Enter**. A dark window opens — that is your
   terminal. Use the **Windows (PowerShell)** commands further down.

**Ubuntu / Linux**
1. Press **Ctrl + Alt + T** (or open *Activities*, type `Terminal`, press **Enter**).
   A window opens.

**How to run a command:** click into the terminal window, paste one line, press
**Enter**, and wait until the text stops scrolling before pasting the next line.
Pasting differs by system:

- macOS: **Cmd + V**
- Windows PowerShell: **Ctrl + V** (or right-click)
- Ubuntu / Linux: **Ctrl + Shift + V** (or right-click)

That is the whole skill. Now do the Quick start below.

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

## Run what you built

opencode writes **real files** into the folder you started it in (`~/vibe` above).
It does not run them for you — you open them yourself. The seminar's first build is a
browser game in a single `index.html`, so "running it" just means opening that file
in your web browser. The loop is always **ask → open → reload**:

1. **Ask.** In opencode, type what you want and press Enter, for example:

   > build a chrome-dino endless runner in one index.html: space to jump, scrolling
   > cacti, collision ends the game, keep a score.

   Wait until it finishes writing `index.html`.

2. **Open it in your browser.** Easiest way, no commands: open your file manager
   (Finder on macOS, Files on Ubuntu, Explorer on Windows), go to the **`vibe`**
   folder in your home directory, and **double-click `index.html`** — it opens in
   your browser and the game runs.

   Prefer the terminal? Open a **second** terminal window (same as Step 0, leave
   opencode running in the first) and run the line for your system:

   ```bash
   open   ~/vibe/index.html   # macOS
   xdg-open ~/vibe/index.html # Ubuntu / Linux
   start  $HOME\vibe\index.html   # Windows (PowerShell)
   ```

3. **Reload.** Want changes? Tell opencode ("make the cacti faster", "add a jump
   sound"), let it rewrite the file, then **reload the browser tab** (Cmd+R on macOS,
   Ctrl+R on Windows/Linux) to see the new version.

Nothing is deployed and nothing goes online — the game is just a file on your
machine, running in your browser, built by a model running on your own laptop.

## What gets installed

| Component | macOS | Linux | Windows |
|---|---|---|---|
| Editor   | brew (micro / zed / vscode)            | apt/dnf/pacman / installer                    | winget                                     |
| Ollama   | Homebrew + `brew services` (autostart) | official installer + `systemctl enable --now` | winget / installer (autostart via Run key) |
| Model    | `qwen3:1.7b` (~1.4 GB, reasoning)      | same                                          | same                                       |
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

Pick a different model. The default **`qwen3:1.7b`** is a small reasoning model: it
shows its thinking before it acts and — unlike the coder-tuned models — reliably calls
the tool that writes your files. Sharper models cost more RAM and a longer download:

```bash
MODEL=qwen3:4b bash bootstrap.sh   # 8 GB+ RAM, sharper, still builds reliably
MODEL=qwen3:8b bash bootstrap.sh   # 16 GB RAM, most reliable builds
MODEL=qwen2.5-coder:0.5b bash bootstrap.sh   # last resort for very weak hardware / slow links; often will not write files
```

On Windows use `$env:EDITOR="zed";` / `$env:MODEL="qwen3:4b";` before the
command.

## Escape hatch: free cloud models (optional, not local)

Small local models are private and offline, but the very smallest ones can still
stumble — describing code in the chat instead of writing the file, or losing the
thread on multi-step tasks. If a laptop simply cannot run a capable local model,
opencode has a built-in hosted gateway, **OpenCode Zen**, with a few **free** models
that are far stronger and write files reliably.

The trade-off is real, and it is the opposite of everything above: these run **in the
cloud, not on your machine**. They need internet, an OpenCode Zen account with an API
key (signup may ask for billing details even for the free tier), and your prompts and
code are sent to their servers. Treat this as an escape hatch for weak hardware, not
the main path — the point of the seminar is making a *local* model succeed.

To use one:

1. Create an account and get an API key at [opencode.ai](https://opencode.ai/)
   (the OpenCode Zen section).
2. In opencode, run `/connect`, choose **OpenCode Zen**, and paste your API key.
3. Run `/models` and pick any model labelled **Free** (the free lineup rotates —
   recent ones include *Big Pickle* and *DeepSeek V4 Flash Free*).

Free access is offered "for a limited time" while the OpenCode team gathers feedback,
so the list changes and may not last. To go back to fully local, `/models` and pick
your Ollama model again.

## Verify it works

```bash
ollama run qwen3:1.7b "write an index.html with a button that shows an alert"   # model answers locally
opencode                                                                               # agent starts, talks to Ollama
```

## Troubleshooting

- **opencode answers with a DeepSeek / "OpenCode Zen" error (e.g. `missing field
  name`) or the status bar shows a cloud model:** opencode is not using your local
  model. Quickest fix inside opencode: run `/models` and pick **Ollama (local)**. To
  make it stick, `~/.config/opencode/opencode.json` needs the line
  `"model": "ollama/qwen3:1.7b"` near the top. If you ran an older version of
  this script the config was written without it (re-running will not add it) — add
  that line yourself, or delete the file and rerun `bootstrap.sh`.
- **`git: command not found` / `git is not recognized`:** git is not installed yet.
  macOS: rerun the `git clone` line and click **Install** on the popup. Windows:
  install it from [git-scm.com](https://git-scm.com/download/win), then open a fresh
  PowerShell window. Ubuntu: `sudo apt-get install -y git`.
- **`ollama` command not found after install (Windows):** open a fresh PowerShell
  window — the installer updates `PATH` for new shells only.
- **Port 11434 already in use:** another Ollama is running. `pkill ollama` (Unix) /
  Task Manager (Windows), then rerun.
- **Model download is slow:** `qwen3:1.7b` is ~1.4 GB; on a very slow link the sub-1 GB
  `MODEL=qwen2.5-coder:0.5b` downloads faster but often will not write files (see the
  model knobs) — or use the cloud escape hatch above.
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
