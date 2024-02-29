# Fireship.io Course

<p align="left">
  <img src="https://yt3.googleusercontent.com/ytc/AIdro_ltOWCZT10fChupyd1atupxII0RoP97CwYGr0Gphw=s176-c-k-c0x00ffffff-no-rj" width="100" />
  <img src="https://cdn0.iconfinder.com/data/icons/octicons/1024/mark-github-1024.png" width="100" />
  <img src="https://git-scm.com/images/logos/downloads/Git-Icon-1788C.png" width="100" />
</p>

## Git Started

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

### VSCODE

- In the file tree you will notice color changes and symbols are added when we modify files, add to staging and commit.
- For more detail info you can view the git icon in the action bar as well as install the GitLens extension ([This one](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)).

  - Within the git dashboard you can see file changes, if they are staged or not, and if you click the file name it will open up a git diff panel.
  - You can also easily stage or un-stage files as well as commit the changes.
  - If you click the ... icon it will list all git commands and allow you to run them without typing them out (This git dashboard UI essentially works like the git desktop app).
  - At the bottom of vscode you will see the current branch name listed. If you click that it will list all of the project branches and allow you to switch between them.

## Remote (GitHub)

### Git Remote

- There are other options for remote collaboration (i.e. Bitbucket and GitLab), but this course will focus on GitHub.
- If you run `git remote -v` it will tell you what repositories you have linked to your project as well as the URLs. Typically the remote repo has the name **origin**.

  - For even more info use `git remote show origin`.

- You can add the project to origin by using the command `git remote add origin https://github.com/your-username/repo-name.git`. You can also configure with SSH, which changes the syntax of the origin URL (i.e. git@ssh-config:your-username/repo-name.git).

### Git Push

- Takes the work in our local repository and syncs it up with our remote repo. This is accomplished with the command `git push origin main` (git push remote-repo-name branch-to-be-pushed).

  - Adding `-u` to the command to set the origin repo to the upstream remote in the .gitconfig file (i.e. `git push origin main -u`). This allows us to use a command (`git pull`) without requiring any additional arguments.

- You can edit on the remote repo in GitHub directly (i.e. pencil icon) and then commit it from there as well. This is good when fixing small typos, for example.

  - This will cause the remote repo to be one commit ahead of the local repo. There is a head at the main branch locally (vscode) and also a head at the main branch on the remote repo. Each of the heads currently have a different commit.

### Git Merge

- When the main branch locally has a different commit than the main branch remotely, there are two ways to merge them together.
- The **first** strategy is to fetch the remote changes then merge the two branches together. To fetch the latest changes locally we run `git fetch`. This downloads the changes but the local code does not reflect the remote code yet.

  - We now need to merge the remote main branch with the local main branch. Click the list of branches on the bottom taskbar in vscode to get the name of remote branch. Then run `git merge origin/main`.
  - The output in the terminal after a merge, you will notice the term **_Fast-Forward_**. That is what is known as a **merge strategy**. This is the simplest strategy to be used when the commits are connected together and you do not need to resolve any merge conflicts. In more complex cases that cannot be easily fast forwarded and additional merge commit will be required to show how the two branches were merged together.

### Git Pull

- The **second** and simpler strategy is to use `git pull`. This command combines fetch and merge.

  - Since we used the `-u` flag during setup, we can use just `git pull`. Without setting upstream we would have to use `git pull origin main`.
  - You can run into issues if you have any un-committed changes in your current working directory and you try a git pull. It will fail, because it is not simply going to overwrite your local changes.
    - The way to fix this issue is to either commit your local changes first OR run `git stash` (To be covered in the advanced sections later in the course).
  - If your local changes are modifying the same line of code as the remote changes being pulled then it could result in a **git conflict** (Also a topic to be covered in later sections of the course).

### Git Clone

- When you have a remote repo that you want to copy or clone down to your local machine. This process copies the remote repo to your local machine, but it also keeps a reference to the original repo, which allows us to use commands such as `git pull` to grab the latest source code from said repo (Also a `git log` will show all previous commits to the remote repo).
- This can be accomplished by the following command `git clone https://github.com/username/repo-name.git` (Or using SSH keys such as the example used in the [Git Remote Section](#git-remote)).

  - You can also add a different name to the directory by appending the name to the end of the above command (i.e. `git clone git@ssh-config:your-username/repo-name.git name-of-dir`).
