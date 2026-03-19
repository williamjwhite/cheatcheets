## Git Cheatsheet

### Setup & Config

| Command | Description | When to use |
|---|---|---|
| `git config --global user.name "Name"` | Set your display name | Once, on a new machine |
| `git config --global user.email "email"` | Set your email | Once, on a new machine |
| `git config --list` | View all config values | Debugging identity or settings issues |
| `git config --global core.editor "code --wait"` | Set VS Code as default editor | Once, on a new machine |

### Creating & Cloning

| Command | Description | When to use |
|---|---|---|
| `git init` | Initialise a new repo in the current directory | Starting a brand new project |
| `git init <dir>` | Initialise a new repo in a named folder | Starting a project in a specific location |
| `git clone <url>` | Clone a remote repo locally | Getting a copy of an existing repo |
| `git clone <url> <dir>` | Clone into a specific folder name | When you want a different local folder name |
| `git clone --depth 1 <url>` | Shallow clone (latest snapshot only) | Large repos where you don't need full history |

### Staging & Committing

| Command | Description | When to use |
|---|---|---|
| `git status` | Show working tree status | Constantly — before every commit |
| `git status -sb` | Short, branch-aware status | Quick glance at what's changed |
| `git add <file>` | Stage a specific file | When you want to commit only part of your changes |
| `git add -A` | Stage all changes (new, modified, deleted) | When everything changed is ready to commit |
| `git add -p` | Interactively stage chunks of changes | When a file has multiple logical changes to split |
| `git commit -m "message"` | Commit with an inline message | Standard commits |
| `git commit --amend --no-edit` | Add staged changes to the last commit silently | Fixing a typo or forgotten file immediately after committing |
| `git commit --amend -m "new message"` | Rewrite the last commit message | Fixing a bad commit message before pushing |
| `git commit --allow-empty -m "message"` | Commit with no changes | Triggering CI, marking a milestone |

### Branching

| Command | Description | When to use |
|---|---|---|
| `git branch` | List local branches | Checking what branches exist |
| `git branch -vv` | List branches with upstream tracking info | Seeing which branches are ahead/behind |
| `git branch -a` | List all branches including remote | Checking what exists on the remote |
| `git branch <name>` | Create a new branch | Creating a feature branch without switching to it |
| `git branch -d <name>` | Delete a merged branch | Cleaning up after a merge |
| `git branch -D <name>` | Force-delete a branch | Discarding an unmerged branch |
| `git branch -m <old> <new>` | Rename a branch | Fixing a branch name |
| `git switch <branch>` | Switch to an existing branch | Modern way to change branches |
| `git switch -c <branch>` | Create and switch to a new branch | Starting work on a new feature |
| `git checkout <branch>` | Switch to a branch (classic syntax) | Same as switch — widely documented |
| `git checkout -b <branch>` | Create and switch to a new branch | Same as `switch -c` |
| `git checkout <commit> -- <file>` | Restore a file from a specific commit | Recovering a deleted or broken file |

### Merging & Rebasing

| Command | Description | When to use |
|---|---|---|
| `git merge <branch>` | Merge a branch into the current branch | Integrating a completed feature |
| `git merge --no-ff <branch>` | Merge with a merge commit even if fast-forward is possible | Preserving branch history visually |
| `git merge --squash <branch>` | Squash all branch commits into one staged change | Keeping main history clean |
| `git merge --abort` | Abort a merge in progress | When a conflict is too complex to resolve now |
| `git rebase <branch>` | Reapply commits on top of another branch | Keeping a feature branch up to date with main |
| `git rebase -i HEAD~<n>` | Interactively rewrite the last n commits | Squashing, reordering, or editing commits before pushing |
| `git rebase --abort` | Abort a rebase in progress | When a rebase goes wrong |
| `git rebase --continue` | Continue after resolving a rebase conflict | Resuming an interrupted rebase |
| `git cherry-pick <commit>` | Apply a specific commit onto the current branch | Porting a bug fix from one branch to another |
| `git cherry-pick <hash1>..<hash2>` | Apply a range of commits | Porting multiple commits at once |

### Remote Repos

| Command | Description | When to use |
|---|---|---|
| `git remote -v` | List remote connections | Checking where push/pull points |
| `git remote add <name> <url>` | Add a remote | Connecting to GitHub after `git init` |
| `git remote remove <name>` | Remove a remote | Cleaning up old remotes |
| `git remote rename <old> <new>` | Rename a remote | Standardising remote names |
| `git fetch` | Download remote changes without merging | Seeing what's changed before pulling |
| `git fetch --all --prune` | Fetch all remotes and remove stale tracking branches | Regular sync and cleanup |
| `git pull` | Fetch and merge remote changes | Getting latest changes on your branch |
| `git pull --rebase` | Fetch and rebase instead of merge | Keeping a linear history on pull |
| `git push` | Push current branch to its upstream | Sharing your commits |
| `git push -u origin <branch>` | Push and set upstream tracking | First push of a new branch |
| `git push --force-with-lease` | Force push only if no one else has pushed | Pushing after a rebase — safer than `--force` |
| `git push origin --delete <branch>` | Delete a remote branch | Cleaning up merged remote branches |

### Undoing & Resetting

| Command | Description | When to use |
|---|---|---|
| `git restore <file>` | Discard uncommitted changes to a file | Throwing away local edits |
| `git restore --staged <file>` | Unstage a file (keep changes) | When you staged something by mistake |
| `git reset HEAD~1 --mixed` | Undo last commit, keep changes unstaged | Redoing a commit with different files or message |
| `git reset HEAD~1 --soft` | Undo last commit, keep changes staged | Redoing a commit message or adding more files |
| `git reset HEAD~1 --hard` | Undo last commit and discard all changes | Completely scrapping the last commit |
| `git reset --hard origin/<branch>` | Reset local branch to match remote exactly | Nuclear option — match remote state |
| `git revert <commit>` | Create a new commit that undoes a previous one | Safely undoing a pushed commit |
| `git clean -fd` | Remove untracked files and directories | Cleaning up build artifacts or temp files |
| `git clean -n` | Dry-run of clean — show what would be deleted | Checking before you clean |

### Stashing

| Command | Description | When to use |
|---|---|---|
| `git stash` | Stash current uncommitted changes | Switching context quickly without committing |
| `git stash save "message"` | Stash with a descriptive label | When you have multiple stashes |
| `git stash pop` | Apply most recent stash and remove it | Resuming stashed work |
| `git stash apply` | Apply most recent stash without removing it | Applying stash to multiple branches |
| `git stash list` | List all stashes | Checking what's stashed |
| `git stash drop stash@{n}` | Delete a specific stash | Cleaning up old stashes |
| `git stash clear` | Delete all stashes | Full stash cleanup |
| `git stash branch <branch>` | Create a new branch from a stash | When stashed changes grew into a feature |

### Viewing History & Diffs

| Command | Description | When to use |
|---|---|---|
| `git log` | Full commit history | Reviewing project history |
| `git log --oneline --graph --decorate` | Compact visual branch graph | Seeing branch structure at a glance |
| `git log -p` | Show commits with their diffs | Detailed audit of what changed and when |
| `git log --author="name"` | Filter commits by author | Reviewing one person's contributions |
| `git log --since="2 weeks ago"` | Filter commits by date | Reviewing recent activity |
| `git log -- <file>` | Show history of a specific file | Tracing when a file changed |
| `git log <branch1>..<branch2>` | Show commits in branch2 not in branch1 | Previewing what a merge will bring in |
| `git diff` | Show unstaged changes | Reviewing work before staging |
| `git diff --staged` | Show staged changes | Reviewing what will be committed |
| `git diff <branch1>..<branch2>` | Compare two branches | Checking what differs between branches |
| `git diff --word-diff` | Show changes at word level instead of line | Reviewing prose or config changes |
| `git show <commit>` | Show a specific commit's changes | Inspecting a single commit |
| `git blame <file>` | Show who last changed each line | Finding who introduced a change |
| `git shortlog -sn` | Summary of commits per author | Team contribution overview |

### Tagging

| Command | Description | When to use |
|---|---|---|
| `git tag` | List all tags | Checking existing releases |
| `git tag <name>` | Create a lightweight tag | Marking a point in history informally |
| `git tag -a <name> -m "message"` | Create an annotated tag | Marking a release with metadata |
| `git push origin <tag>` | Push a tag to remote | Publishing a release tag |
| `git push origin --tags` | Push all tags | Syncing all local tags to remote |
| `git tag -d <name>` | Delete a local tag | Removing a mistaken tag |
| `git push origin --delete <tag>` | Delete a remote tag | Removing a published tag |

### Searching

| Command | Description | When to use |
|---|---|---|
| `git grep "<pattern>"` | Search working tree for a string | Finding where something is used in code |
| `git log -S "<string>"` | Find commits that added/removed a string | Tracking when a line of code appeared or disappeared |
| `git log --grep="<pattern>"` | Search commit messages | Finding a commit by keyword |
| `git bisect start` | Start a binary search for a bug-introducing commit | Hunting down a regression |
| `git bisect good <commit>` | Mark a commit as good during bisect | Narrowing the bisect range |
| `git bisect bad <commit>` | Mark a commit as bad during bisect | Narrowing the bisect range |
| `git bisect reset` | End a bisect session | After finding the culprit commit |

### Submodules

| Command | Description | When to use |
|---|---|---|
| `git submodule add <url>` | Add a repo as a submodule | Including a dependency as a pinned sub-repo |
| `git submodule init` | Initialise submodules after cloning | First setup of a repo that uses submodules |
| `git submodule update --init --recursive` | Fetch and update all submodules | After cloning or pulling submodule changes |
| `git submodule foreach git pull` | Pull latest in all submodules | Updating all dependencies at once |

### Aliases (from .gitconfig)

| Alias | Expands to | When to use |
|---|---|---|
| `git s` | `git status -sb` | Quick status check |
| `git l` | `git log --oneline --graph --decorate -15` | Visual history snapshot |
| `git la` | `git log --oneline --graph --decorate --all` | Full branch graph |
| `git c "msg"` | `git commit -m` | Fast commit |
| `git ca` | `git commit --amend --no-edit` | Quietly fix last commit |
| `git pf` | `git push --force-with-lease` | Safe force push after rebase |
| `git undo` | `git reset HEAD~1 --mixed` | Undo last commit, keep changes |
| `git unstage <file>` | `git restore --staged` | Remove file from staging area |
| `git discard <file>` | `git restore` | Throw away working tree changes |
| `git whoami` | `git config user.email` | Confirm which identity is active |
| `git root` | `git rev-parse --show-toplevel` | Jump to repo root in scripts |
