# Phase 0: Development Environment Setup Notes

## What we built

- A working Windows development environment for Python
- A Git repository for the project, with `main` as the stable branch
- A project virtual environment (`.venv`)
- A `.gitignore` and an initial `README.md`

## Environment findings

- Python 3.14.6 is installed **twice**: `C:\Python314` (classic installer, what `python` runs) and the Python install manager copy (what `py` runs). Both work, and we left both installed.
- A third `python.exe` in `WindowsApps` is a Microsoft Store stub. It only opens the Store and can be ignored.
- VS Code and Git were already installed, and the Git name and email were already configured.
- The Python, Pylance and debugpy VS Code extensions were already installed.

## Key concepts

**PATH.** A list of folders Windows searches when you type a command. The first match wins, which is why `python` ran `C:\Python314`.

**Virtual environment.** An isolated copy of the Python setup with its own packages. Activating it puts its `Scripts` folder first on PATH, so `python` and `pip` mean the project's versions. This is what makes the two global Pythons irrelevant.

**The three Git areas.** Working directory (your files), staging area (changes chosen for the next commit), repository (permanent history). `git add` moves changes to staging, and `git commit` saves them to the repository.

**Branch.** A lightweight pointer to a commit. `HEAD` points at the branch you're currently on.

**`.gitignore`.** Patterns Git should never track. It keeps `.venv/`, caches and, most importantly, `.env` (future secrets) out of the repo. Python 3.13+ also puts its own `.gitignore` inside `.venv`, but ours stays as an explicit, visible safeguard.

## Problems and how we handled them

- **Duplicate Pythons:** isolated the project in a venv instead of uninstalling anything. Rule: install packages with pip only while `(.venv)` shows in the prompt.
- **PowerShell blocking `Activate.ps1`:** VS Code ran `Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned`, which changes the policy for that terminal window only.
- **Code Runner extension:** it runs files with whatever `python` is on PATH, ignoring the selected venv. Run code from the terminal or VS Code's own Run button instead.

## Commands used

| Command                                       | Purpose                                  |
| --------------------------------------------- | ---------------------------------------- |
| `python --version`                            | Check the Python version on PATH         |
| `py -0p`                                      | List Pythons known to the launcher       |
| `where.exe python`                            | List every `python.exe` on PATH          |
| `python -m pip --version`                     | Show which Python pip belongs to         |
| `git config --global init.defaultBranch main` | Make new repos start on `main`           |
| `git init`                                    | Create a repository                      |
| `python -m venv .venv`                        | Create the virtual environment           |
| `git add <file>` / `git commit -m "..."`      | Stage and commit                         |
| `git switch -c <branch>`                      | Create and switch to a branch            |
| `git log --oneline --all --graph`             | View history of all branches             |
| `git diff --stat main..HEAD`                  | Summarize differences between two tips   |
| `git remote add origin <url>`                 | Connects to Github                       |
| `git remote -v`                               | List remote repositories                 |
| `git push -u origin <branch>`                 | Pushes a branch to GitHub.               |
| `git switch main`                             | Switch to main                           |
| `git merge <branch>`                          | Mergers a branch into the current branch |

## GitHub and merging

**Remote.** A named URL pointing at another copy of the repository. `origin` is only the conventional name for the main one. `git remote add origin <url>` creates it, and `git remote -v` lists remotes.

**Push.** `git push -u origin <branch>` uploads a branch. `-u` links the local branch to its remote counterpart, so later `git push` and `git pull` need no arguments. Authentication goes through Git Credential Manager, not a typed password.

**Why the GitHub repo was created empty.** Adding a README or `.gitignore` on GitHub would create a second, unrelated history that must be reconciled before pushing.

**Fast-forward merge.** `git switch main` then `git merge <branch>`. If `main` has no commits the branch lacks, Git only moves the `main` pointer forward. No merge commit and no conflicts are possible. When both branches have new commits, Git creates a merge commit with two parents.

**`main..HEAD` vs `main...HEAD`.** For `git log`, two dots means commits reachable from HEAD but not from `main`. For `git diff`, two dots compares the two tips directly, while three dots compares HEAD against the common ancestor. Use three dots to review what a branch adds.

## Commit history for this phase

- `e61ed14` chore: add .gitignore
- `dee00ef` docs: add initial README
- `4f267cf` docs: add Phase 0 setup notes
- `2870b3b` docs: add GitHub and merge notes to Phase 0 notes

## How Phase 0 connects forward

Every later phase starts from a stable `main`, works on its own branch, and installs packages inside this venv. Phase 1 adds the first Python code.

## Interview questions

1. What is a virtual environment, and what problem does it solve?
2. What does PATH do, and why can a machine have several Pythons?
3. What are Git's working directory, staging area and repository?
4. What is a branch, and what does HEAD point to?
5. What is the difference between `git diff main..HEAD` and `git diff main...HEAD`?
6. Why should `.env` be in `.gitignore` before the file exists?
