## Work with a Remote "Teacher" Repository

1. Go to the folder of the project you are working on and initialize a git repository:

  ```bash
  git init
  ```

2. Add a remote repository named "teacher" with the corresponding URL (ask the teacher of that day):

  ```bash
  git remote add teacher [URL]
  ```

3. Fetch the last status of that repo:

  ```bash
  git fetch teacher
  ```

4. Update you current directory with the last status of master, or any specific commit by SHA:

  ```bash
  git reset --hard teacher/master
  git reset --hard [SHA]
  ```
