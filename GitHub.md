# What is Git?

Git is version control system tools used to track changes in your code (track code).

* Popular
* Free & Open Source
* Fast & Scalable

**Features:**

* Track history
* Helps to collaborate with project worker

---

# What is GitHub?

GitHub is cloud platform used to store source code in the form of repositories (folder).

Website that allow developers to store and their code using Git.

In this, changes = **commit**

---

# What is Repository?

It is folder or storage location used to store source code, files, and the history of changes.

---

# What is Token?

Token is secret key that allows your computer or application to access your GitHub account without using your real password.

**Create Token:**

* Profile Pic
* Settings
* Developer Settings
* Personal Access Tokens
* Tokens (Classic)
* Generate Token

> **Note:** Do **not** upload or share your personal GitHub token in a public repository. It gives access to your GitHub account.

---

# Git Configuration Commands

```bash
git config --global user.name "sonu"
git config --global user.email "bhavanaghule23@gmail.com"

git config user.name
git config user.email

git config --list
```

---

# What is Origin?

Origin is nickname (alias) for the remote repository URL.

```bash
git clone "url"

git add ./filename

git commit -m "one file xyz added"

git push origin main
```

After that they will ask you the password then enter the token.

---

# Clone & Status

## Clone

Cloning a repository on our local machine.

```bash
git clone <some link>
```

It helps to connect your project to the server.

## Status

Displaying the states of the code.

```bash
git status
```

When we uses remote and local:

* Remote = GitHub
* Local = Laptop/PC

### Status of Git

* **Untracked** – New files that Git doesn't yet track.
* **Modified** – Changed but not staged.
* **Staged** – File is ready to be committed.
* **Unmodified** – Unchanged.
* **Committed** – Saved history.

---

# Add & Commit

## Add

Adds new or changed files in your working directory to the Git staging area.

```bash
git add <filename>
```

## Commit

It is the record of change.

```bash
git commit -m "some message"
```

---

# Push Command

Push = upload local repo content to remote repo.

```bash
git push origin main
```

---

# Create Repo

See you want to add the repository and file in the GitHub without clone so just create the folder and just run following commands through that.

## Init Command

Init = used to create a new Git repo.

```bash
git init

git remote add origin <link>

git remote -v          // to verify remote

git branch             // to check branch

git branch -M main     // to rename branch

git push origin main
```

---

# Branch Command

Branch means the path where independently developer working on project at same time without affecting each other and waiting for each other and also one thing after creating completion we can merge the branches.

It use to create independent copy of the code so developers can work safely without affecting main projects.

```bash
git branch                              // to check branch

git branch <branch name>                // to create the branch

git branch -m main                      // to rename branch

git checkout <branch name>              // to navigate means changing the branch

git checkout -b <branch name>           // creating new branch

git branch -d <branch name>             // to delete branch

git push origin <branch name>           // to push branch into the GitHub

git push origin --delete <branch name>  // to delete branch from the remote server as well as local
```

---

# Merging Code

## Way 1

```bash
git diff <branch name>      // to compare commits, branches, files & more

git merge <branch name>     // to merge 2 branches
```

## Way 2

Create a PR (Pull Request).

**Pull Request:** It lets you tell others about changes you've pushed to branch in a repository on GitHub.

---

# Pull Command

```bash
git pull origin main
```

Used to fetch and download content from a remote repo and immediately update the local repo to match that content.

---

# Resolving Merge Conflicts

An event that takes place when Git is unable to automatically resolve differences in code between two commits.

---

# Undoing Changes

## Case 1: Staged Changes (add zalet)

```bash
git reset <file name>

git reset
```

## Case 2: Committed Changes (for one commit)

```bash
git reset HEAD~1
```

## Case 3: Committed Changes (for many commits)

```bash
git reset <commit hash>
```

This is for undo the changes in remote server (GitHub).

```bash
git reset --hard <commit hash>
```

This for undo the committed changes in the local server also.

---

# Fork

A fork a new repository that shares code and visibility settings with the original "upstream" repository.

Fork is a rough copy.


