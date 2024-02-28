# Fireship.io Course

<p align="left">
  <img src="https://yt3.googleusercontent.com/ytc/AIdro_ltOWCZT10fChupyd1atupxII0RoP97CwYGr0Gphw=s176-c-k-c0x00ffffff-no-rj" width="100" />
  <img src="https://cdn0.iconfinder.com/data/icons/octicons/1024/mark-github-1024.png" width="100" />
  <img src="https://git-scm.com/images/logos/downloads/Git-Icon-1788C.png" width="100" />
</p>

## Git & GitHub

### Definitions

**_The Head_** - Represents the most recent commit. There is an ID assigned to each commit, which allows you to always revert back to it.

**_Branch_** - Removes your work and commits from the master/main branch. Created by running `git branch && git checkout <branch_name>`. Once work is completed in the branch you move back to the master/main branch by running `git checkout && git merge <branch_name>`. This makes the tip of your branch the head of the master/main branch.

### Git Install Instructions

- Run `git --version` in the terminal. If this does not work then you need to install git.

  - On Windows, use the installer or go through the WSL/Git setup (See: [WSL Setup and Git](https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-git)).
  - On Mac, there is also an installer, but it might be better to use a tool such as Homebrew (See: [Homebrew Installation](https://brew.sh/) and run `brew install git`).

- Run `git config --list` to modify our current git config. This list should have a user name and a user email.

  - If no user name, run `git config --global user.name "replace_with_github_username".`
  - If no user email, run `git config --global user.email "replace_with_github_email".`

### Git Init

- Once you create a project, `cd` into the project directory and run `git init` to initialize the project as a Github repository.

### Git Status

- Running `git status` will provide a message on the current state of the repo. These are things such as which files are added or deleted or modified, which branch you are on, and if you made any commits.

  - You will see if a file is **untracked**. This means that the current file has not been committed to the repo yet so git is not keeping track of the difference (diff) between file changes.
  - You can create a `.gitignore` file to ignore files or directories within the repo. These will not be tracked.

### Staging

- Before committing file changes to the repo you need to send them to the staging area. This is done using `git add .` (The . adds all files to staging, but you can specify by writing out the file name instead of the period).

  - If you want to remove files from staging before committing them you can run `git reset .`.

### Commit

- Every commit has a unique ID that git can use to track the difference in those files versus the difference in some other commit.
- This allows you to be able to roll back to a previous commit if, for example, a bug is introduced to your code.
- You can perform a commit by running `git commit -m "Your commit message goes here."`. After the commit, and if you staged all file changes, you will have a clean working directory.
- You can also skip the step of adding to staging and combine the add/commit in one command as follows `git add -a -m "Your commit message goes here."`.

  - To get info about the last commit you can run `git log`. This will provide you with the ID, author, and timestamp. You will also see the commit referencing the **head** on the master/main branch. The head is the most current commit on a branch ([See definitions](#definitions)).
