[Watch here a movie version of this exercise.](https://www.youtube.com/watch?v=iZcvWkbxzeU)

## Project set up

1. Create local repository and first commit:

  ```bash
  git init
  git add .
  git commit -m "First commit"
  ```

2. Add remote repository in GH:

  ```bash
  git remote add origin git@github.com:miriamtocino/world-of-conflicts.git
  git push -u origin master
  ```

## Working on a feature branch

1. Create a new feature branch:

  ```bash
  git checkout -b feature-branch
  ```

2. Do some changes in the branch, commit them and push them to GH in your own branch.

  ```bash
  git add .
  git commit -m "Changes in feature branch"
  git push origin feature-branch
  ```

3. Go to GH and create a pull request for that branch. Two things can happen when you do that:

  - You are allowed to merge your branch
  - You are NOT allowed to merge your branch

## Resolve conflicts

If you are not allowed to merge your branch in master, you need to rebase your feature branch locally.

1. Checkout into your feature-branch:

  ```bash
  git checkout feature-branch
  ```

2. Fetch origin and rebase your branch with master:

  ```bash
  git fetch origin && git rebase origin/master
  ```

3. Here is where you might be getting conflicts. Open up your merge tool to fix them:

  ```bash
  git mergetool
  ```

Note: Every mergetool is different, so whatever you are using, make sure that the final version of the file is what you want.

Note: Don't forget to save your files in your mergetool and quit the program completely: Cmd + Q in Mac.

4. Once you are out of the mergetool, you need to tell git to continue rebasing:

  ```bash
  git rebase --continue
  ```

5. Two things can happen here:

- You don't have more conflicts, you are ready here!
- You have more conflicts to be resolved. Go ahead and repeat the process above for every conflict you get.

## Update remote feature branch

Since you did a rebase of your branch locally and changed some of your commits, you still need to push that version of your branch to GH.

Actually what we want is to overwrite whatever is in GH at the moment, so we need to "force" the push:

1. Push your branch to remote repo, forcing the operation.

  ```bash
  git push origin feature-branch -f
  ```

2. Refresh the page in GH, review files that changed and check if everything is as you expected it to be. Now you should be able to merge your branch.

3. Back in your terminal, checkout master, fetch origin and pull latest version of master branch.

  ```bash
  git checkout master
  git fetch
  git pull origin master
  ```

4. As a sanity check, let's run git status:

  ```
  git status
  # no changes, nothing to commit
  ```

5. Delete your feature branch locally:

  ```bash
  git branch -d feature-branch
  ```

## Your database got updated

1. If another member of the team made changes in the database, you need to run the migrations to update your local database:

  ```bash
  rake db:migrate
  ```

2. When you do that, your schema.rb file will get updated but you want to discard those changes. Do it by running:

  ```bash
  git checkout -- db/schema.rb
  ```
