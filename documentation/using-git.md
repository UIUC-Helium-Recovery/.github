# Using Git for Version Control

- **Author**: Luke Marren
- **Recent Updates**:
  - Date: 6-2-25
  - Maintainer(s): Luke Marren

## Table of Contents

- [What is Git?](#what-is-git)
    - [Basic Overview](#basic-overview)
    - [Main Uses of Git](#main-uses-of-git)
- [Starting with Git](#starting-with-git)
    - [Copying a Remote Git Repository via SSH](#copying-a-remote-git-repository-via-ssh)
    - [Steps](#steps)
- [Continuous Development with Git](#continuous-development-with-git)
    - [Practical Workflows](#practical-workflows)
    - [Macro Workflow: Issue, Branch, Code, Pull Request, Merge](#macro-workflow-issue-branch-code-pull-request-merge)
    - [Constant Workflow: Branch, Checkout, Fetch, Diff, Cherrypick, Merge](#constant-workflow-branch-checkout-fetch-diff-cherrypick-merge)
    - [Micro Workflow: Status, Add, Status, Commit, Push](#micro-workflow-status-add-status-commit-push)
- [When Something Breaks: Reverting Changes Using Git](#when-something-breaks-reverting-changes-using-git)
    - [Step One: Don't Panic](#step-one-dont-panic)

## What is Git?

### Basic Overview
Git is a powerful version control software that tracks every change you make on every file a Git repository is initiated in.

### Main Uses of Git

Git is used to:

- Track file changes so that developers can revert to older software versions if needed
- Backup files on GitHub by linking to a remote repository
- Ensure teams of developers don't trample on each others' code and can seemlessly review team code before deploying it or sending it back to the drawing board.

## Starting with Git

### Copying a Remote Git Repository via SSH

**Note**: This guide assumes you have SSH set up on your computer for accessing your GitHub account. If you do not have this set up, go to Luke's SOP on SSHing in the box.

Since all of the Helium Recovery Project's repos are already made, it's best to copy the organization's repos directly from GitHub using SSH.

### Steps

Here's a walk-through on doing the above:

1. In your terminal, navigate to the directory (e.g., `/User/work/`) you'd like to put our organization's repositories (except for `RPis` - see separate documentation for accessing that repo) into.
2. At the root of that repository (i.e., inside `/User/work/` and not a child directory of it), type the following command in your terminal, replacing `repo-name` with either `.github`, or `medusa`:

```git clone git@github.com:UIUC-Helium-Recovery/repo-name.git```

3. The above command should clone the specified repo into a new folder with the same name as the repo.
    - E.g., if you cloned `medusa`, then you should be able to see it using the `ls` command. The aboslute path to this folder would be `/User/work/medusa/`.
4. Go inside the new directory using the `cd` command.
5. "Fetch" all the branches on the remote repo using `git fetch origin`
    - This makes your local Git repo aware of all the branches on the remote repo *and* it clones the main/default repo (e.g., `cPanel` from `medusa`).
6. Display the remote branches you now can track on your local repo using `git branch -r`
7. If you'd like to have a copy of a specific branch on the remote, like `dev`, run `git checkout dev`.

Repeat these steps for all three of our organization's repositories.

## Continuous Development with Git

### Practical Workflows

Now that you've got local copies of the organization's repos, you can begin *safely* editing code.

Here's a workflow we should all adhere to while developing to ensure we don't

- Blow up the system
- Step on people's toes
- Trigger the end of the world: a merge conflict

### Macro Workflow: Issue, Branch, Code, Pull Request, Merge

Whenever you want to change something that will eventually directly affect how the Pis or the website works, follow this workflow.

**Note**: All of this is done in GitHub (aside from the coding part).

1. Issue
    - Create an issue on the GitHub that describes the problem you're trying to solve so other people know it exists and, more importantly, that you or someone else is working on it.
2. Branch
    - Create a feature branch from the issue off of the repo's main/default branch. It's helpful to keep the long name of the issue (e.g., 24-add-function-docstrings-to-pipe_problem.py - this is not a real issue we made btw) for when you want to look back through our repo's commit history.
3. Code (follow the [constant](#constant-workflow-fetch-diff-cherrypick-merge) and [micro](#micro-workflow-status-add-status-commit-push) workflows)
    - Develop your code while adhering to proper coding standards (i.e., test frequently and use tools like a debugger, linter, formatter, ... ,etc.)
4. Pull Request
    - When you're ready to add your code back to the `main/default` branch, go to the GitHub, submit a pull request for your branch and the `dev` branch (**not** the main/default just yet), and notify coworkers of your work (text/email them). Make sure your `pull request` adequately summarizes the changes you made to your feature branch.
5. Merge (or go back to the drawing board)
    - When everyone has checked over the pull-request, approved of them, and resolved potential `merge conflicts`, go ahead and put the pull request through.

If no issues seem to arise on the `dev` branch, pull the `dev` branch to the `main/default`.

### Constant Workflow: Branch, Checkout, Fetch, Diff, Cherrypick

After you've created a feature branch, make sure to check for updates to the parent branch you branched off of frequently to stay up-to-date with the latest changes upstream.

1. Branch
    - The command `git branch -a` shows you all the local branches and locally-tracked remote branches that are on your machine. Use this to ensure that you are on your feature branch and *not* coding on someone else's or, even worse, the `dev` or `main/default` branches.
2. Checkout
    - If you're not on your feature branch/the branch you intend to edit, run the command `git checkout [YOUR BRANCH]` to switch to your branch.
3. Fetch
    - The command `git fetch --prune origin` "fetches" all the changes made to the remote repository since you copied/last updated it onto your local machine.
    - If any branches on the remote were added, deleted (hence the `--prune` flag), or changed, you now have the ability to copy their latest versions and you've already let go of outdated (deleted) remote branches.
4. Diff
    - The command `git diff [YOUR BRANCH] origin[/MAIN BRANCH]` (replacing the bracketed arguments) will show the changes made between your local branch's files and the remote's main branch's files. When you're done viewing the differences in the terminal, press `q` and then hit `ENTER`.
    - **Note**: you can change the arguments to compare differences between different branches, commits, staged and unstaged changes.
    - **Note**: I highly recommend using VS Code's version control tab to view the differences. It is *much*, *much* easier to understand your version history this way.
5. Cherrypick
    - If you encounter newer commits that show changes which don't interfere with the changes you made on your feature branch, feel free to run the command `git cherry-pick [COMMIT HASH]` to merge that commit's changes into your branch.
    - **Note** only do this if you are absolutely sure that there are no conflicting or out-dated differences between that commit and your branch in its current state. Do this using `git fetch origin/[SPECIFIED BRANCH]` and `git diff [YOUR BRANCH] origin/[SPECIFIED BRANCH]`.

### Micro Workflow: Status, Add, Status, Commit, Push

When working locally on your feature branch and trying to ensure the remote feature branch reflects what you have currently (a best practice), do the following frequently:

1. Status
    - Running `git status` shows you if you have any untracked or unstaged (not added to be commited and pushed) changes on your local machine. Staged changes will be in green and untracked/unstaged changes will be in red.
2. Add
    - If there's a change you'd like to add to be committed, add it using `git add [FILENAME]`.
    - If you'd like to do this for all untracked/unstaged changes in your repo, run the command `git add .`.
    - Alternatively, you can list as many filenames out as you'd like.
3. Status
    - Run `git status` again to check if the changes you want to be tracked are in green.
    - It's a good idea to run git status very frequently so you remember to commit early and often.
4. Commit
    - When you're ready to package your changes up to be sent to the remote GitHub repository, run `git commit -m "[AN INFORMATIVE MESSAGE]"`.
    - This packages up all the changes you staged using `git add [FILENAME(s) or .]` so that they can be sent to GitHub.
    - **Note**: I *strongly* encourage you to add individual files separately *and* commit them separately so that you aren't parsing through or reverting to commits with multi-file changes because that can mess things up very easily and is hard to understand/keep track of.
5. Push
    - When you're ready to send your commits to GitHub, run `git push`.

## When Something Breaks: Reverting Changes Using Git

### Step One: Don't Panic

Excluding John and Dom, we've all destroyed one part of the system of another. I.e., I have destroyed parts of the system before.

But worry not! As long as you did not go onto the GitHub and delete the main/default branch, your changes may be reverted.

**TODO**
