```shell
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

### 1. Starting a Project

These commands are used when you are either starting a brand-new project or bringing an existing project from a server (like GitHub) onto your computer.

| Command | Description |
| --- | --- |
| `git init` | Initializes a brand-new, empty Git repository in your current folder. |
| `git clone [url]` | Downloads an existing project from a remote URL to your computer. |

---

### 2. The Staging Workflow

Git uses a "Three-Tree" architecture: your working directory, the staging area (index), and the history (commit). Use these commands to move changes through that pipeline.

| Command | Description |
| --- | --- |
| `git status` | Shows which files have been modified and which are currently staged. |
| `git add [file]` | Adds a specific file to the staging area (prepares it for a commit). |
| `git add .` | Adds **all** changed files in the current directory to the staging area. |
| `git commit -m "[message]"` | Saves your staged changes into the version history with a descriptive note. |

---

### 3. Branching & Merging

Branches allow you to work on new features or bug fixes without breaking the "main" (stable) version of your code.

| Command | Description |
| --- | --- |
| `git branch` | Lists all local branches in your repository. |
| `git branch [name]` | Creates a new branch with the specified name. |
| `git checkout [name]` | Switches your workspace to the specified branch. |
| `git checkout -b [name]` | Shortcut to create a new branch and switch to it immediately. |
| `git merge [branch]` | Joins the history of the specified branch into your current branch. |

---

### 4. Remote Syncing

These commands allow you to share your work with others and pull in updates that teammates have made.

| Command | Description |
| --- | --- |
| `git remote add origin [url]` | Links your local repository to a remote server (like GitHub). |
| `git push origin [branch]` | Uploads your local commits to the remote repository. |
| `git pull` | Fetches changes from the remote server and merges them into your current branch. |
| `git fetch` | Downloads updates from the remote server but does **not** merge them yet. |

---

### 5. Reviewing History

| Command | Description |
| --- | --- |
| `git log` | Displays a chronological list of all commits made in the project. |
| `git diff` | Shows the specific line-by-line changes made to files that aren't yet staged. |

