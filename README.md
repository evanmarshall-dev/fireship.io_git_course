# Fireship.io Course

<p align="left">
  <img src="https://yt3.googleusercontent.com/ytc/AIdro_ltOWCZT10fChupyd1atupxII0RoP97CwYGr0Gphw=s176-c-k-c0x00ffffff-no-rj" width="100" />
  <img src="https://cdn0.iconfinder.com/data/icons/octicons/1024/mark-github-1024.png" width="100" />
  <img src="https://git-scm.com/images/logos/downloads/Git-Icon-1788C.png" width="100" />
</p>

## GIT STARTED

### Definitions

**_The Head_** - Represents the most recent commit. There is an ID assigned to each commit, which allows you to always revert back to it.

**_Branch_** - Removes your work and commits from the master/main branch. Created by running `git branch && git checkout <branch_name>`. Once work is completed in the branch you move back to the master/main branch by running `git checkout && git merge <branch_name>`. This makes the tip of your branch the head of the master/main branch.

### Git Install Instructions

- Run `git --version` in the terminal. If this does not work then you need to install git.

  - On Windows, use the installer or go through the WSL/Git setup (See: [WSL Setup and Git](https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-git)).
  - On Mac, there is also an installer, but it might be better to use a tool such as Homebrew (See: [Homebrew Installation](https://brew.sh/) and run `brew install git`).

- Run `git config --list` to modify our current git config. This list should have a user name and a user email.

  - If no user name, run `git config --global user.name "<replace_with_github_username>"`.
  - If no user email, run `git config --global user.email "<replace_with_github_email>"`.

### Git Init

- Once you create a project, `cd` into the project directory and run `git init` to initialize the project as a Github repository.

### Git Status

- Running `git status` will provide a message on the current state of the repo. These are things such as which files are added or deleted or modified, which branch you are on, and if you made any commits.

  - You will see if a file is **untracked**. This means that the current file has not been committed to the repo yet so git is not keeping track of the difference (diff) between file changes.
  - You can create a `.gitignore` file to ignore files or directories within the repo. These will not be tracked.

### Staging

- Before committing file changes to the repo you need to send them to the staging area. This is done using `git add .` (The `.` adds all files to staging, but you can specify by writing out the file name instead of the period).

  - If you want to remove files from staging before committing them you can run `git reset .`.

### Commit

- Every commit has a unique ID that git can use to track the difference in those files versus the difference in some other commit.
- This allows you to be able to roll back to a previous commit if, for example, a bug is introduced to your code.
- You can perform a commit by running `git commit -m "<Your commit message goes here.>"`. After the commit, and if you staged all file changes, you will have a clean working directory.
- You can also skip the step of adding to staging and combine the add/commit in one command as follows `git add -a -m "<Your commit message goes here.>"`.

  - To get info about the last commit you can run `git log`. This will provide you with the ID, author, and timestamp. You will also see the commit referencing the **head** on the master/main branch. The head is the most current commit on a branch ([See definitions](#definitions)).

### VSCODE

- In the file tree you will notice color changes and symbols are added when we modify files, add to staging and commit.
- For more detail info you can view the git icon in the action bar as well as install the GitLens extension ([This one](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)).

  - Within the git dashboard you can see file changes, if they are staged or not, and if you click the file name it will open up a git diff panel.
  - You can also easily stage or un-stage files as well as commit the changes.
  - If you click the `...` icon it will list all git commands and allow you to run them without typing them out (This git dashboard UI essentially works like the git desktop app).
  - At the bottom of vscode you will see the current branch name listed. If you click that it will list all of the project branches and allow you to switch between them.

## REMOTE (GitHub)

### Git Remote

- There are other options for remote collaboration (i.e. Bitbucket and GitLab), but this course will focus on GitHub.
- If you run `git remote -v` it will tell you what repositories you have linked to your project as well as the URLs. Typically the remote repo has the name **origin**.

  - For even more info use `git remote show origin`.

- You can add the project to origin by using the command `git remote add origin https://github.com/<your-username>/<repo-name>.git`. You can also configure with SSH, which changes the syntax of the origin URL (i.e. `git@ssh-config:<your-username>/<repo-name>.git`).

### Git Push

- Takes the work in our local repository and syncs it up with our remote repo. This is accomplished with the command `git push origin main` (`git push <remote-repo-name> <branch-to-be-pushed>`).

  - Adding `-u` to the command to set the origin repo to the upstream remote in the `.gitconfig` file (i.e. `git push origin main -u`). This allows us to use a command (`git pull`) without requiring any additional arguments.

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
- This can be accomplished by the following command `git clone https://github.com/<username>/<repo-name>.git` (Or using SSH keys such as the example used in the [Git Remote Section](#git-remote)).

  - You can also add a different name to the directory by appending the name to the end of the above command (i.e. `git clone git@ssh-config:<your-username>/<repo-name>.git <name-of-dir>`).

### GitHub Codespaces

- While you are browsing the remote repo on GitHub, if you hit `.` it will open a cloud-based version of vscode. This is another useful strategy for small changes that you do not want to have to deal with on your local machine.
- You cannot use terminal in the cloud-based vscode, but if you try to access it you do receive the option to use the terminal in **codespaces** (This is basically vscode running a virtual machine (VM) with the necessary dependencies to run your app).

  - You can configure codespaces to use as much memory and computing power as you need.

## COLLABORATION

### Git Branch

- Branching allows multiple developers to work on different app features in isolation from the main branch. Branches are also good for solo developers who want to experiment with a feature without polluting the master/main branch.

- To list all current branches in a project write `git branch`.

  - It is common to rename the master branch to main and this is accomplished by running `git branch -M main`.

  - If you want to create a branch run `git branch <new-branch-name>`.

  - If you want to delete a branch run `git branch -d <new-branch-name>`. If you use a `-D` when you run the branch deletion then it will delete the branch even if there is changes on it and it has been merged into the main branch.

### Git Checkout

- Just creating the branch does not move you into the created branch. To do this you need to run `git checkout <branch-name>`.

- You can commit the changes and the branch to the remote repo by running `git commit -am "<Your commit message here.>"`.

- If you switch back to the main branch prior to merging then the code you created on the branch will disappear.

- If you are on the main branch and you want to both create a new branch and checkout the new branch in one command you would run `git checkout -b <new-branch-name>`.

### Merge Conflicts

- A conflict occurs when you try to merge two different branches that modify the same line of code and have been committed. Under these circumstances git does not know which one to use.

- In vscode any files affected by the conflict will be highlighted in red and the lines affected will be displayed in different colors. You can also go to the terminal and run `git diff` to see the same display within the terminal window.

  - The outcome to the conflict will be to accept the changes in one of the two branches or merge the changes which will put them one line below the other.

  - If you accept the changes then you need to create a new commit called a **merge commit**. You commit the merge the same way you would normally commit changes however it is good practice to label somewhere in the commit message that it is for a merge.

- If you want to go back to the original state prior to the merge starting then you can run `git merge --abort`.

### Fork

- Similar to git clone, forking is more of a GitHub thing. You would fork a repo if you want to contribute to an open source project and push your own copy of the code hosted on GitHub.

- It copies the project to your own GitHub account and allows you to make changes to it without affecting the original. It still maintains a link to the original repo so that you can fetch updates.

- Common practice is to work on a new feature in the forked repo then send a **_pull request_** to merge that new code into the original repo. The author of the original can then review your changes and decide if they want to merge your code or not.

### Pull Request

1. Find a GitHub repo you want to contribute to.
2. Fork the repo (maintains a link to the original upstream repo).
3. Clone the fork onto your local system.
4. Open up project on your local machine and create a branch that describes the changes you are going to make.
5. Use `git checkout` to switch into the new branch.
6. After you complete the changes, `git add` and `git commit` to commit them to the repo.
7. Then push up to the repo using `git push origin <your-feature-branch-name>`.
8. Go back to the repo on GitHub and click the button to create a new pull request.
9. Make sure you follow the contribution guidelines to the original repo owner carefully.
10. Click the green button to submit the pull request.

- When working with the fork locally you can keep it in sync with the original repo by running:

  - `git remote add upstream https://github.com/<original-username>/<original-repo-name>.git`. This adds a remote link to the upstream repo.
  - When there are changes run `git fetch upstream`.
  - Then run `git rebase upstream/main` to apply changes on top of your existing work.

## Advanced

### Git Reset

- If you want to get rid of everything in the staging area run `git reset`. This does not modify or delete anything.

- If you commit a bad file change then you need to first grab the ID or SHA of that commit using `git log`. Then you find the commit you want to go back to and run `git reset <your-commit-id>`.

  - By default git reset will run in **mixed mode**, which means that it will move us back to the previous commit, but it will not delete the files that we were working on.

- If you want to revert back to the previous commit AND delete the changes (go back to the state of the previous commit) you would run `git reset --hard <your-commit-id>`. Be careful using this because you cannot retrieve the deleted file changes after this command.

- **_NEVER_** do a reset when a commit has been pushed to GitHub.

### Git Revert

- Since you should never use `git reset` on commits already pushed to GitHub, there is a command to do this without causing issues for everyone working on the GitHub repo.

  - The command is `git revert`.

    - First, you want to run `git log` to get the ID of the bad commit.
    - Run `git revert <commit ID>`, which removes the committed file similar to `git reset --hard`. The **difference** is that the bad commit is not lost and is still in the commit history. A `git log` will show a new commit which states that we reverted the bad commit.
    - This commit can now be pushed to the remote repo (GitHub).

### Git Commit --Amend

- If you make a minor mistake in git (i.e. typo in a commit message or you forgot to stage a file with your commit) you can modify it without needing to reset or revert.

- This only works in some specific situations.

  - For fixing a commit message, run `git commit --amend -m "<fixed message>"`.
  - For adding an un-staged file and not amend the message, run `git add . && git commit --amend --no-edit`.

### Git Stash

- Git stash allows you to save your work without having to commit it to the repositories history. This is useful if you are working on something experimental, which does not need to be committed, but you still want to work on it later.

  - Run `git stash` and you will see the content will be removed from the file, but is not lost. Instead, it was saved to the stash which is like an array which holds onto changes that can be applied later.

  - To apply those changes back to the code run `git stash pop`.

- If you find yourself doing this frequently you might want to add additional info about each item in the stash.

  - If you want to do this then first run `git stash save <info or name about the feature>`.

  - You can see all the current items you have in the stash by running `git stash list`. This will show you that each item has an index followed by the name that you provided.

  - Above, when we used `git stash pop` it only used the latest stashed item. If you want to do this out of order then you would run `git stash apply <index number that you want to apply to your code>` (The index number is found by running the `git stash list` command).

- You want to use `git stash` sparingly, because you might get merge conflicts when the stashed items affect the same line of code.

### Git Rebase

- **Rebase** vs. **Merge**. Merge is when someone works on a feature branch and merges it back into the master/main branch. Rebase is when we take a feature branch and rewrite history to make it look like you started working on the feature branch with the latest updates of the master/main branch or some other branch you rebased.

  - Rebase keeps your feature branch up to date with the master/main branch without extra merge commits.

- Rebase should only really be done when you are working on your own private feature branch, because it is a more **destructive** option that rewrites history. You do not want to do it with a public branch with multiple collaborator because everyone would be working with a different history.

  - First, create a feature branch by running `git checkout -b <feature branch name>`.

  - Add a file and commit the branch.

  - Make commits on the master/main branch.

  - On the feature branch we want to integrate the new code from the master/main with what we are working on.

    - We can use `git merge`, but the problem is we might have to add a bunch of merge commits to the history, which clutters up the history of a larger project.

  - Instead, we can run `git rebase main`, which takes the feature branch and puts it on the tip of the main. This makes it look like you just started working on the feature with the code from the master/main branch.

    - If you are ever unsure about a rebase, you can make another branch from the feature, rebase that, and if it all works out then delete that extra branch and perform the rebase on the feature branch.

### Squash

- Another thing you can do with rebase is **_squash_** your commits. Often when working on a feature you make lots of commits which were not necessary when the feature gets merged onto the master/main branch. These commits are irrelevant to the rest of the team.

- Squashing the commits take them and combine them into one single commit with a single message.

  - This is done by running `git rebase main --interactive` that pulls up a document in the editor that allows us to customize how this rebase will work.

    - You will see the commits listed in the editor with the keyword **_pick_** beside them. Pick is the default and means you want to keep the commit as is. To squash any of the commits you will change pick to **squash** which takes the commit messages from each of these commits and combine them into one single message with the original commit.
    - You can also use **_fixup_**, which does the same thing but it discards the commit message from the commits you squash in.
    - You then save the file and close it, which brings up another file where you can customize the commit message.

  - A `git log` command will now show one commit with one commit message.

  - This is the last thing you do before performing a pull request or merge your feature back into the master/main branch.

### GitHub Actions

- A tool to automate repetitive and/or manual processes (DevOps your app).

- Considering a repo on GitHub, people might star the repo, create a pull request, create an issue, or merge code into the master/main branch. These are all examples of **_events_** and any event can trigger an automated workflow.

- A workflow can spin up one or more containers for you in the cloud and you provide a set of steps or instructions for the container to do something useful for you.

- GitHub will log the progress of each step and make it very clear if something failed.

- Instead of using action steps created manually, you can use ones implemented by the community. Each step is essentially a reusable chunk of code called an **_action_**.

- The following is some real world examples of actions.

#### Continuous Integration (CI)

The idea behind CI is to have developers submit their code to the main codebase in small maintainable chunks. Usually this is done on a daily basis and those changes should be automatically **tested** against the main codebase.

When you look at a project on GitHub you will see an **actions** tab. This is where you find a log of everything that happened on the server when a workflow is triggered.

What we want to do for CI is to have our test suite run every time there is pull request to the master/main branch. If the test suite fails we will get a red "x" automatically telling us not to merge that pull request. If every thing goes as planned we will get a green check mark.

In the repo or project you will see a .github directory with a sub-directory called **_workflows_** and a file within it called `integrate.yml`. Anything within the workflows directory will be picked up by GitHub and automatically setup as a workflow in the cloud. The yaml file is where we define the workflow.

Here is a sample yaml file:

```yaml
name: Node Continuous Integration

# Tell it on which event(s) to run with the on object.
on:
  # Run on pull request.
  pull_request:
    # To the main branch.
    branches: [main]

# Every workflow has one or more jobs defined by the jobs object.
jobs:
  # Give the job a name.
  test_pull_request:
    # Tell the job which virtual machine (VM) to run on (i.e. Ubuntu, Windows or MacOS).
    runs-on: ubuntu-latest
    # Give the job a set of steps/instructions that build and test the code.
    steps:
      # First get source code into the VM using an officially maintained action called checkout. This brings your source code into the working directory.
      # This allows you to run commands like you would from the command line if working on the project locally.
      - uses: actions/checkout@v2
      # We also need to setup nodejs to run those commands. We use the node setup action.
      - uses: actions/setup-node@v1
        with:
          # And specify the version.
          node-version: 12
      # Now we can start running our own commands. First, install all of our dependencies from npm, which is equivalent to npm install, but it does a clean install for your CI server.
      - run: npm ci
      # Then run our test command to test our code.
      - run: npm test
      # Then run our build command to make sure the build compiles properly.
      - run: npm run build
```

To start using the workflow we simply commit it to the master/main branch (i.e. git add, git commit, git push).

The actions tab on GitHub will remain empty until a pull request event triggers our workflow (create branch, make some changes (breaking or not), git add, git commit, git push, then run the pull request on GitHub).

If it was a breaking change and the pull request workflow fails then you can return to the local code, fix it, re-commit/push it and GitHub will auto re-run the workflow because it is an open pull request.

#### Continuous Deployment (CD)
