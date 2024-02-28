# Fireship.io Course

![Fireship.io Logo](https://yt3.googleusercontent.com/ytc/AIdro_ltOWCZT10fChupyd1atupxII0RoP97CwYGr0Gphw=s176-c-k-c0x00ffffff-no-rj)

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
