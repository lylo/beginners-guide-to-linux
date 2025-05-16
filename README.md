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

We're using **Ubuntu**, a popular and beginner-friendly Linux distributions. Other distributiosns include Fedora, Arch, and Debian (Ubuntu is based on Debian and has a large community, making it easy to find help).

### 🚪 Why WSL?

WSL lets you run Linux **inside Windows**, without needing to dual boot or use a virtual machine. It gives you the best of both worlds.

---

### 🔧 Installing WSL and Ubuntu

#### Step 1: Open PowerShell as Administrator

PowerShell is a command-line shell built by Microsoft for system administration. Unlike the older Command Prompt (cmd.exe), PowerShell gives you access to a more powerful set of commands. It's the recommended tool for installing and managing WSL on Windows.

To open it, search for "PowerShell", right-click it, and select **Run as Administrator**.

#### Step 2: Install WSL with a single command

Type this command into PowerShell:

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

> **Note:** The user you create during this setup is not a full superuser by default, but it can use `sudo` to perform administrative tasks. This is a common practice in Linux to enhance security. We'll cover `sudo` in the next section.

---

## 💻 2. Exploring Linux: Terminal, Filesystem, and Core Concepts

### 🖥️ What is the Terminal?

The terminal (also called the **command line**) is where you type commands to navigate the file system, edit files and run programs, instead of clicking around a user interface. It's incredibly powerful, and learning it will make you a more effective coder and researcher.

#### What is a Shell?

A shell is the program that actually processes the command you type in. Think of the terminal as the window, and the shell as the interpreter that understands and executes the commands you type. Common shells include:

- **Bash** (Bourne Again Shell): The default in most Linux distributions including Ubuntu
- **Zsh** (Z Shell): Now the default in macOS, with more features than Bash
- **Fish**: A user-friendly shell with syntax highlighting and autosuggestions

When you see commands in this guide, we're using the Bash shell, which is what you'll get by default in Ubuntu.

When you open a terminal you'll usually see a prompt like:
```
yourname@machine:~$
```

The line you see before each command is called the **prompt**. It shows information like your username, computer name, and current folder. In this example, the `~` means you're in your **home folder** (`~` is a shortcut for `/home/yourname`).

This command prompt can be customized, but that's a topic for another day.

---

### 🗂 The Linux Filesystem: Key Directories

Linux has a different file structure from Windows. For example, instead of `C:\Program Files` for applications and `C:\Users\YourName` for your files, Linux uses folders like `/usr` for software and `/home/yourname` for your personal files.

Here's a quick reference:

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

**Why are they called `/bin`, `/usr`, and `/etc`?**

- **`/bin`** stands for "binaries" — it contains essential programs needed to start and run the system.
- **`/usr`** originally meant "user" but now holds most user-installed software and libraries (think of it like "Unix System Resources").
- **`/etc`** comes from "et cetera" — it's a place for system-wide configuration files and settings.

You don’t need to memorize all these, but knowing `/home`, `/etc`, and `/usr` gives you a great start.

---

### 🧭 Useful Terminal Commands

Here are some use commands for navigating and managing files in the terminal. You can type them directly into the terminal to try them out.

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

#### Files vs Directories

- A **file** is a document or program (like `notes.txt` or `hello.py`).
- A **directory** (or folder) is a container for files and other directories.

In the terminal:
- `.` means "the current directory"
- `..` means "the parent directory" (one level up)

#### Command Flags

Many commands accept **flags** (also called options or switches) to change their behavior. Flags usually start with a dash (`-`). For example:

```bash
ls -l      # List files in long format (shows permissions, size, date, etc.)
ls -a      # List all files, including hidden ones (those starting with .)
rm -r dir  # Remove a directory and its contents recursively
```

You can combine flags, like `ls -la` to list all files in long format.

To see all the options for a command, use the `man` (manual) command. You'll see a lot of information, but don't be overwhelmed! Type:

```bash
man ls
```

This opens the manual page for `ls`. Use the arrow keys to scroll, and press `q` to quit.

Now try creating a folder, creating an empty file (`touch`), then list the contents of the folder:
```bash
mkdir physics
cd physics
touch notes.txt
ls -l
```
---

### 🛡️ Beginner Guide to File Permissions

To view file permissions (i.e. **who can read, write, or execute a file**), use the `ls -l` command. For example:
```bash
ls -l
```

You'll see output like this:
```
-rwxr-xr-- 1 user group 1234 Jan 1 12:00 myfile
```

Here's what it means:
- The first character (`-`) indicates the type of file (`-` for regular files, `d` for directories).
- The next nine characters (`rwxr-xr--`) show permissions:
  - **rwx**: Owner can read, write, and execute.
  - **r-x**: Group can read and execute.
  - **r--**: Others can only read.

### 👤 What Are User and Group?

- **User:** The owner of the file. This is usually the person who created the file.
- **Group:** A collection of users who share access to the file. For example, a team working on the same project might belong to the same group.

Each file belongs to one user and one group. Permissions are defined separately for the user, the group, and others (everyone else).

### 🔧 Changing Permissions

To change permissions, use the `chmod` command. For example:
```bash
chmod u+x myfile   # Add execute permission for the owner
chmod g-w myfile   # Remove write permission for the group
chmod o+r myfile   # Add read permission for others
```

You can also set permissions using numbers:
```bash
chmod 755 myfile   # Owner: rwx, Group: r-x, Others: r-x
```

### 🔑 Changing Ownership

To change the owner or group of a file, use the `chown` command:
```bash
sudo chown newuser myfile   # Change owner to 'newuser'
sudo chown newuser:newgroup myfile   # Change owner and group
```

Practice these commands to get comfortable with managing file permissions!
#### 🔒 The `sudo` command

You'll start to notice that many commands are prefixed with `sudo`. This is important, but what does it mean?

 The `sudo` command stands for "superuser do." It temporarily gives you administrative privileges to perform tasks that require higher permissions, such as installing or removing software. You'll often see `sudo` at the beginning of commands in this section.

---

## 📦 3. Installing Software on Ubuntu

### 🛠️ What Are Packages?

In Linux, software is distributed as **packages**. A package is a compressed file that contains the program, its dependencies, and metadata (like version information). Packages make it easy to install, update, and remove software.

### 📦 Package Management Systems

Ubuntu uses a package management system to handle software installation and updates. The most common tools are:

- **APT (Advanced Package Tool):** The default package manager for Ubuntu. It works with `.deb` packages.
- **Snap:** A newer system for installing software in isolated containers. Useful for cross-distribution compatibility.

### 🔧 Installing a Package with APT

To install a package using APT, use the `sudo apt install` command. For example, to install the `htop` system monitor:

```bash
sudo apt update    # Update the list of available packages
sudo apt install htop
```

### 🔄 Updating Ubuntu

Keeping your system up to date is important for security and stability. To update all installed packages and the system itself, run:

```bash
sudo apt update    # Refresh the list of available updates
sudo apt upgrade   # Install the updates
```

### 🗑️ Removing a Package

If you no longer need a package, you can remove it with:

```bash
sudo apt remove packagename
```

For example, to remove `htop`:

```bash
sudo apt remove htop
```

---

## 🧰 4. Text Editors

### 🖋️ What are text editors?

Text editors are essential tools for working with code and configuration files in Linux. They allow you to create, edit, and save plain text files. Here are three popular editors:

- **Nano**: A simple, beginner-friendly editor that works in the terminal.
- **Vi/Vim**: A powerful, advanced editor with a steep learning curve. It's available on almost every Linux system.
- **VS Code**: A modern, *graphical* editor with many features for coding, writing, and debugging.

It's good to know the basics of nano and Vi, but as a beginner, you might prefer using VS Code for larger projects and coding tasks.

---

### 🖥️ Install VS Code for WSL

1. Download VS Code from: [https://code.visualstudio.com](https://code.visualstudio.com)
2. Open Ubuntu and run:
   ```bash
   code .
   ```
   The first time you run this, it will prompt you to install the **Remote - WSL** extension.

### ✨ Key Features of VS Code

- Open folders/files with `code .`
- Works seamlessly with Python, LaTeX, Git, and Markdown
- Syntax highlighting and code completion for many languages
- Includes a built-in terminal for running commands
- Beginner-friendly and highly customizable with a wide range of extensions

---

### 🛠 Nano: A Terminal-Based Text Editor

Nano is a simple text editor that works directly in the terminal. To open a file with Nano:
```bash
nano filename.txt
```

- **Save changes**: Press `Ctrl+O`, then `Enter`.
- **Exit**: Press `Ctrl+X`.

---

### ⚙️ Vi or Vim: A Powerful but Advanced Editor

Vi (or its improved version, Vim) is a lightweight editor available on all Linux systems. To open a file with Vi:
```bash
vi filename.txt
```

- **Insert mode**: Press `i` to start editing.
- **Command mode**: Press `Esc` to stop editing.
- **Save and exit**: Type `:wq` and press `Enter`.

If you're curious about learning Vi in-depth, check out the [Vim Adventures](https://vim-adventures.com/) game, which teaches you Vi commands through a fun adventure.

---

## 🧪 5. Install Python

Python is widely used in physics and scientific computing. To install Python and its package manager (pip), run:

```bash
sudo apt install python3 python3-pip
```

### ✅ Check Python Installation

Verify that Python is installed by checking its version:
```bash
python3 --version
```

### 📝 Create and Run a Simple Python Script

1. Create a new Python file using a text editor:
   ```bash
   nano hello.py
   ```
2. Add the following code:
   ```python
   print("Hello, physics!")
   ```
3. Save and exit (in Nano, press `Ctrl+O`, then `Enter`, and `Ctrl+X`).

4. Run the script:
   ```bash
   python3 hello.py
   ```

You should see:
```
Hello, physics!
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

GitHub is a web app where you can store your Git repositories (repos) online. It lets you:

- Store your code in the cloud using Git
- Collaborate with others on projects
- Share code and work across devices

Think: Git is the tool. GitHub is the platform. There are other platforms like GitLab and Bitbucket, but GitHub is the most popular.

---

### 📦 What is a Repository (Repo)?

A **repo** is just a folder tracked by Git. It contains:
- Your files
- The full history of changes
- Optional remote links (e.g. to GitHub)

---

### 🔧 Install Git

To install Git on Ubuntu, open your terminal and run:

```bash
sudo apt install git
```

You can configure Git with your name and email (this is important for when you make commits):

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

---

### 🧪 Create Your First Git Repo

1. Create a new directory (folder) in your home directoy for your project and create a new file in it.

```bash
cd ~                 # ensure your in your home directory
mkdir myproject      # create a directory called myproject
cd myproject         # change into that directory
touch readme.md      # create a new file called readme.md
```

2. Make this folder 'git aware' by initializing it as a Git repository.

```bash
git init             # initialize a new Git repository in this location
```

3. Add files to the repository and commit them.

- **`git add`** adds files to the **staging area**, which is like a "to-do list" for changes you want to include in your next commit. It doesn't _save_ the changes yet, but marks them as _ready to be saved_.
- **`git commit`**: This command saves the changes in the staging area to the repository. Each commit is like a snapshot of your project at a specific point in time. You can include a message (`-m`) to describe what changes were made.

```bash
git add .            # add all files to the staging area
git commit -m "Initial commit"  # commit the changes with a message
```

---

### 🔗 Push the repo to GitHub

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

## ✍️ 7. Writing Markdown Notes

### 💡 What is Markdown?

Markdown is a plain text format for writing notes with **headings, bold text, links, and even equations**. It's perfect for lab notes, documentation, and studying. GitHub uses Markdown for README files, and Jupyter Notebooks use it for text cells.

📚 Official guide: [https://www.markdownguide.org](https://www.markdownguide.org)

---

### 🧪 Example Markdown File

Here's a simple example of a Markdown file. You can create it using any text editor.

```bash

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

## 📄 8. Write Beautiful Scientific Documents with LaTeX

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
- [x] Install and use VS Code
- [x] Learn basic file permissions and change them
- [x] Install and test Python
- [x] Set up Git and push a project to GitHub
- [x] Write a Markdown note
- [x] Compile a LaTeX document to PDF

---

## 📚 Learning Resources

Here are some beginner-friendly resources to help you deepen your understanding of Linux, coding, and related tools:

- 📘 [The Missing Semester of Your CS Education (MIT)](https://missing.csail.mit.edu/)
  A free course from MIT that covers essential computer science topics often overlooked in traditional curricula, such as the command line, version control, and shell scripting.

- 🧠 [Markdown Guide](https://www.markdownguide.org/)
  A comprehensive guide to Markdown, a lightweight markup language for formatting text. Perfect for writing README files, notes, and documentation.

- 🔧 [Learn Git Branching (interactive site)](https://learngitbranching.js.org/)
  An interactive website that teaches Git concepts visually. Great for beginners who want to understand branching, merging, and other Git workflows.

- 🐍 [Python for Everybody (free course)](https://www.py4e.com/)
  A beginner-friendly Python course that covers the basics of programming and data manipulation. Includes free videos, exercises, and a textbook.

- ✍️ [Obsidian Starter Vault](https://publish.obsidian.md/start-here/)
  A guide to getting started with Obsidian, a powerful Markdown-based note-taking app. Ideal for organizing your notes and ideas.

- 📺 [Linux Journey](https://linuxjourney.com/)
  A free, interactive website that teaches Linux concepts step-by-step. Covers everything from basic commands to advanced topics like networking.

- 🛠️ [VS Code Documentation](https://code.visualstudio.com/docs)
  Official documentation for Visual Studio Code. Learn how to use its features, extensions, and integrations for coding, debugging, and more.

- 📂 [Introduction to the Linux File System](https://linuxhandbook.com/linux-directory-structure/)
  A beginner-friendly guide to understanding the Linux file system and its key directories.

- 🎮 [Vim Adventures](https://vim-adventures.com/)
  A fun, interactive game that teaches you how to use Vim, a powerful text editor, through an engaging adventure.

- 🌐 [OverTheWire: Bandit](https://overthewire.org/wargames/bandit/)
  A beginner-friendly wargame that teaches Linux command-line skills through challenges. Perfect for practicing what you've learned.
