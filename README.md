# 🧑‍🔬 Beginner's guide to Ubuntu, Terminal, Git and coding tools

Welcome! This guide teaches you how to use the tools of modern science: Linux, the terminal, version control, programming, and writing documents with Markdown and LaTeX. It's aimed at smart beginners who want to understand what they're doing — not just copy-paste commands.

---

## 🛠️ 1. Install Ubuntu with WSL (Windows Subsystem for Linux)

### 🌍 Why Linux?

Linux is the standard platform for scientific computing, coding, and research because it's:

- Free and open-source
- Stable, fast, and efficient
- Scriptable and automatable
- Built for power users and developers

We're using **Ubuntu**, a popular and beginner-friendly Linux distribution.

### 🚪 Why WSL?

WSL lets you run Linux **inside Windows**, without needing to dual boot or use a virtual machine. It gives you the best of both worlds.

---

### 🔧 Installing WSL and Ubuntu

#### Step 1: Open PowerShell as Administrator
Search for “PowerShell”, right-click it, and select **Run as Administrator**.

#### Step 2: Install WSL with a single command
```powershell
wsl --install
```
This will:
- Enable the WSL feature
- Install WSL version 2 (WSL2), which uses a real Linux kernel
- Install the latest Ubuntu by default

You’ll need to **restart your computer** when prompted.

#### Step 3: Set up Ubuntu
After restarting, launch Ubuntu from the Start menu. On first launch, it will ask you to:
- Create a **username** (this is your Linux user)
- Set a **password** (used for admin actions like updates)

---

## 💻 2. Exploring Linux: Terminal, Filesystem, and Core Concepts

### 🖥️ What is the Terminal?

The terminal (also called the **command line**) is where you type commands instead of clicking around. It's incredibly powerful, and learning it will make you a more effective coder and researcher.

You’ll usually see a prompt like:
```
yourname@machine:~$
```
The `~` means you're in your **home folder**.

---

### 🗂 The Linux Filesystem: Key Directories

Linux has a different layout from Windows. Here's a quick reference:

| Directory | What It’s For |
|-----------|----------------|
| `/`       | The root (top-level) directory — everything lives under here |
| `/home`   | Personal folders for users (like `C:\Users\`) |
| `/etc`    | System-wide configuration files (like settings) |
| `/usr`    | User-installed software and libraries |
| `/bin`    | Essential command-line programs |
| `/var`    | Variable data (like logs and databases) |
| `/tmp`    | Temporary files that may be deleted on reboot |
| `/mnt`    | Where external drives and Windows disks are mounted (e.g. `/mnt/c` for C:\ drive) |

You don’t need to memorize all these, but knowing `/home`, `/etc`, and `/usr` gives you a great start.

---

### 🧭 Useful Terminal Commands

```bash
pwd        # Print current directory (path)
ls         # List files in current directory
cd         # Change directory
cd ..      # Go up one level
mkdir test # Create a folder called test
rm file    # Remove a file
mv old new # Rename or move files
cp a b     # Copy a to b
```

Try this:
```bash
mkdir physics
cd physics
touch notes.txt
ls
```

---

## ✍️ 3. Writing Markdown Notes

### 💡 What is Markdown?

Markdown is a plain text format for writing notes with **headings, bold text, links, and even equations**. It's perfect for lab notes, documentation, and studying.

Used by:
- Obsidian (note-taking)
- GitHub (readmes)
- Jupyter Notebooks (code + text)

📚 Official guide: [https://www.markdownguide.org](https://www.markdownguide.org)

---

### 🧪 Example Markdown File

```markdown
# Heading 1
The largest heading. Like `<h1>` in HTML.

## Heading 2
Subheading, like `<h2>`.

### Lists and Emphasis
- Bullet point
- Another item

**Bold**, *italic*, `inline code`

### Equations
You can include equations using LaTeX-style math:
$$
E = mc^2
$$
```

Save this as `notes.md`. Try opening it in **VS Code** (`code notes.md`) to see syntax highlighting and previews.

---

## 🧰 4. Editors: VS Code, Nano, and Vi

### 📝 VS Code (Visual Studio Code)

A modern, graphical editor. Great for coding, Markdown, LaTeX, and Python.

**Run it from the Ubuntu terminal:**
```bash
code .
```

> The first time you run this, it will install the **Remote - WSL** extension so VS Code can work inside Ubuntu.

---

### 🛠 Nano: A Terminal-Based Text Editor

```bash
nano filename.txt
```
- Simple and beginner-friendly
- Use Ctrl+O to save, Ctrl+X to exit

---

### ⚙️ Vi or Vim: A Powerful but Advanced Editor

```bash
vi filename.txt
```
- Lightweight, always available
- Steep learning curve (starts in "command mode")
- Press `i` to insert, `Esc` to return to command mode, then `:wq` to write and quit

---

## 🐍 5. Install Python and Run Your First Script

### 🧪 Install Python and Pip

Ubuntu usually includes Python, but run this just in case:
```bash
sudo apt install python3 python3-pip
```

---

### ✨ Create and Run a Script Using VS Code

1. Open VS Code in your folder:
   ```bash
   code .
   ```
2. Create a file: `hello.py`
3. Paste this:
   ```python
   print("Hello, physics world!")
   ```
4. Save and run:
   ```bash
   python3 hello.py
   ```

---

## 🧬 6. Version Control with Git and GitHub

### 🧠 What is Git?

Git is a **version control system** — it tracks changes to your code and files over time. You can:

- Undo mistakes
- Collaborate with others
- See who changed what, and when

👨‍🔧 Created by **Linus Torvalds**, who also created Linux.

---

### ☁️ What is GitHub?

GitHub is a website where you can store your Git repositories (repos) online. It lets you:

- Back up your projects
- Collaborate with others
- Share code and work across devices

Think: Git is the tool. GitHub is the platform.

---

### 📦 What is a Repository (Repo)?

A **repo** is just a folder tracked by Git. It contains:
- Your files
- The full history of changes
- Optional remote links (e.g. to GitHub)

---

### 🔧 Install Git

```bash
sudo apt install git
```

Then configure it:
```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

---

### 🧪 Create Your First Git Repo

```bash
mkdir myproject
cd myproject
git init
touch readme.md
git add .
git commit -m "Initial commit"
```

---

### 🔗 Push It to GitHub

1. Create a GitHub account: [https://github.com](https://github.com)
2. Click **New Repository**
3. Follow the instructions to connect your local project:

```bash
git remote add origin https://github.com/yourusername/myproject.git
git branch -M main
git push -u origin main
```

> Tip: GitHub now uses personal access tokens instead of passwords for pushing changes.

---

## 📄 7. Write Beautiful Scientific Documents with LaTeX

### 🧪 Install LaTeX

```bash
sudo apt install texlive-full
```

---

### 📄 A Sample Document

Save this as `equation.tex`:

```latex
\documentclass{article}
\usepackage{amsmath}
\begin{document}

Here is Einstein’s famous equation:

\[
E = mc^2
\]

\end{document}
```

Compile it:
```bash
pdflatex equation.tex
```

---

## ⚡ Bonus Tools & Aliases

| Tool | Purpose |
|------|---------|
| `htop` | Visual system monitor (like Task Manager) |
| `grep` | Search inside files |
| `find` | Search for files and folders |
| `alias` | Create shortcuts for commands |

### Example: Add an Alias

Open `.bashrc`:
```bash
nano ~/.bashrc
```

Add:
```bash
alias gs='git status'
```

Then apply it:
```bash
source ~/.bashrc
```

---

## ✅ What to Practice This Week

- [x] Install Ubuntu and WSL
- [x] Explore folders and commands in the terminal
- [x] Install and test Python
- [x] Write a Markdown note
- [x] Set up Git and push a project to GitHub
- [x] Compile a LaTeX document to PDF

---

## 📚 Learning Resources

- 📘 [The Missing Semester of Your CS Education (MIT)](https://missing.csail.mit.edu/)
- 🧠 [Markdown Guide](https://www.markdownguide.org/)
- 🔧 [Learn Git Branching (interactive site)](https://learngitbranching.js.org/)
- 🐍 [Python for Everybody (free course)](https://www.py4e.com/)
- ✍️ [Obsidian Starter Vault](https://publish.obsidian.md/start-here/)
