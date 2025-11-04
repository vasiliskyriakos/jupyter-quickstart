# newjupyter

A tiny bash script that scaffolds a **ready‑to‑run Python + Jupyter + VS Code** project on macOS. One command creates the folder, venv (or conda), installs Jupyter + basics, drops a starter notebook + script, and opens the project in VS Code.

---

## ✨ Features
- Project skeleton: `.vscode/`, `notebooks/`, `scripts/`, `src/`, `.gitignore`, `README.md`.
- Python **venv** (default) or **conda** (with `--conda`).
- Installs **jupyter**, **ipykernel**, and core libs (`numpy`, `pandas`, `matplotlib`, `scikit-learn`).
- Starter notebook with a small procedural‑art demo + environment check.
- Lightweight environment check script (`scripts/script.py`).
- Opens the project in VS Code (reuses window if already open).

---

## 🧩 Requirements
- macOS
- **Python 3.9+** available as `python3`
- **VS Code** (and ideally the `code` CLI: *VS Code → Command Palette → "Shell Command: Install 'code' command in PATH"*)
- **make** (comes with macOS command line tools)
- (optional) **Homebrew** if you want to install GitHub CLI (`gh`)

---

## 📦 Installation (local script)

> Pick one location in your PATH. Common choices:
> - `~/bin` (create it if it doesn’t exist)
> - `/usr/local/bin` (requires sudo)

```bash
# 1) Clone your repo (or drop the script file somewhere) and cd into it
#    If you already have the file locally, just skip to step 3
# git clone https://github.com/<you>/<repo>.git
# cd <repo>

# 2) Make the script executable
chmod +x newjupyter

# 3) Put it somewhere in your PATH (choose one)
mkdir -p ~/bin
cp newjupyter ~/bin/

# 4) Ensure ~/bin is in PATH (add to shell profile if needed)
#    For zsh (default on macOS):
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc

# 5) Test
which newjupyter
newjupyter --help || true
```

**Tip:** If you prefer `/usr/local/bin`:
```bash
sudo cp newjupyter /usr/local/bin/
```

---

## 🚀 Usage
Create a new project in the current directory:
```bash
newjupyter myproject
```
Flags:
```text
--no-open            Do not open VS Code after setup
--conda              Use conda instead of venv
--python=/path/to/python3  Use a specific Python binary
```
Examples:
```bash
# Use system python3, open VS Code when done
newjupyter ds-notes

# Use a specific Python
newjupyter --python=/usr/local/bin/python3.11 my-nb

# Conda mode
newjupyter --conda research-lab

# Just create, don’t open VS Code
newjupyter --no-open scratchpad
```

What you get:
```
myproject/
├─ .vscode/settings.json
├─ notebooks/starter.ipynb
├─ scripts/script.py
├─ src/
├─ requirements.txt
├─ Makefile
├─ .gitignore
└─ README.md
```

---

## 🧪 After creation
```bash
cd myproject
make setup     # (already run by the script for venv mode)
make run       # runs scripts/script.py sanity check
make notebook  # starts Jupyter Notebook using this venv
```

If the notebook kernel doesn’t appear in VS Code:
```bash
make kernel
```

---

## ☁️ Publish the project to GitHub (optional)
With GitHub CLI (`brew install gh`):
```bash
cd myproject
make github-setup        # once per machine (installs gh & login)
make github-publish-gh   # init git, create remote, push main
```

Manual git (without `gh`):
```bash
cd myproject
git init -b main
git add .
git commit -m "Initial commit"
# create an empty repo at github.com first, then:
git remote add origin https://github.com/<you>/<repo>.git
git push -u origin main
```

---

## 🔧 Troubleshooting
- **`code: command not found`** → In VS Code, run *Shell Command: Install 'code' command in PATH*.
- **VS Code opens the wrong window** → run `code -n .` inside the project folder.
- **Pip uses system Python** → run `make setup` (ensures venv is used).
- **Conda kernel missing** → `python -m ipykernel install --user --name myenv --display-name "Python (myenv)"` in that env.

---

## 📝 License
MIT (or your preferred license).