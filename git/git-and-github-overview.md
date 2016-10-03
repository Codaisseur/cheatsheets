## Setup

_Configuring user information used across all local repositories._

Set a name that is identifiable for credit when review version history:

```bash
git config --global user.name "[firstname lastname]"
```

Set an email address that will be associated with each history maker:

```bash
git config --global user.email "[valid-email]"
```

Set automatic command line coloring for Git for easy reviewing:

```bash
git config --global color.ui auto
```

## Initialization

_Starting a new repository or obtaining from an external resource._

Initialize an existing directory as a Git repository:

```bash
git init
```

Retrieve an entire repository from a hosted location via URL:

```bash
git clone [url]
```

## Stage & Snapshot

_Working with snapshots and the Git staging area._

Show modified files in working directory staged for your next commit:

```bash
git status
```

Add a file as it looks now to your next commit (stage):

```bash
git add [file]
```

Unstage a file while retaining the changes in working directory:

```bash
git reset [file]
```

Diff of what is staged but not yet commited:

```bash
git diff
```

Diff of what is staged but not yet committed:

```bash
git diff --staged
```

Commit your staged content as a new commit snapshot:

```bash
git commit -m "[descriptive message]"
```

## Branch & Merge

_Isolating work in branches, changing context, and integrating changes._

List your branches. A * will appear next to the currently active branch:

```bash
git branch
```

Create a new branch at the current commit:

```bash
git branch [branch-name]
```

Switch to another branch and check it out into your working directory:

```bash
git checkout [branch-name]
```

Merge the specific branch's history into the current one:

```bash
git merge [branch-name]
```

Show all commits in the current branch's history:

```bash
git log
```

## Inspect & Compare

_Examining logs, diffs and object information._

Show the commit history for the current active branch:

```bash
git log
```

Show the commits on branchA that are not on branchB:

```bash
git log branchB..branchA
```

Show the commits that changed file, even across renames:

```bash
git log --follow [file]
```

Show the diff of what is in branchA that is not in branchB:

```bash
git diff branchB..branchA
```

Show any object in Git in human-readable format:

```bash
git show [SHA]
```

## Tracking Path Changes

_Versioning file removes and path changes._

Delete the file from project and stage the removal for commit:

```bash
git rm [file]
```

Change an existing file path and stage the move:

```bash
git mv [existing-path] [new-path]
```

Show all commit logs with indication of any paths that moved:

```bash
git log --stat -M
```

## Ignoring Patterns

_Preventing unintentional staging or committing of files._

Save a file with desired patterns as `.gitignore` with either direct string matches or wildcard globs:

```bash
logs
*.notes
pattern*/
```

System wide ignore pattern for all local repositories:

```bash
git config --global core.excludesfile [file]
```

## Share & Update

_Retrieving updates from another repository and updating local repos._

Add a git URL as an alias:

```bash
git remote add [alias] [url]
```

Fetch down all the branches from that Git remote:

```bash
git fetch [alias]
```

Merge a remote branch into your current branch to bring it up to date:

```bash
git merge [alias]/[branch]
```

Transmit local branch commits to the remote repository branch:

```bash
git push [alias] [branch]
```

Fetch and merge any commits from the tracking remote branch:

```bash
git pull
```

## Rewrite History

_Rewriting branches, updating commits and clearing history._

Apply any commits of current branch ahead of specified one:

```bash
git rebase [branch]
```

Clear staging area, rewrite working tree from specified commit:

```bash
git reset --hard [commit]
```

## Temporary Commits

_Temporarily store modified, tracked files in order to change branches._

Save modified and staged changes:

```bash
git stash
```

List stack-order of stashed file changes:

```bash
git stash list
```

Write working branch from top of stash stack:

```bash
git stash pop
```

Discard the changes from top of stash stack:

```bash
git stash drop
```
