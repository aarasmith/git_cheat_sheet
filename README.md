# Git Cheat Sheet

A cheat sheet for common use cases

## Table of Contents
1. [Working Tree and Local vs. Remote Changes](#1-working-tree-and-local-vs-remote-changes)
2. [Setting VSCode as the Core Editor](#2-setting-vscode-as-the-core-editor)
3. [Restoring a File to its Last Commit](#3-restoring-a-file-to-its-last-commit)
4. [Git Status](#4-git-status)
5. [Restoring a Deleted File](#5-restoring-a-deleted-file)
6. [Returning to a Previous Revision](#6-returning-to-a-previous-revision)
7. [Restoring a Single File](#7-restoring-a-single-file)
8. [Explaining the Reflog](#8-explaining-the-reflog)
9. [Explaining Rebasing](#9-explaining-rebasing)
10. [Adding a New Git Remote and Checking Out an Existing Feature Branch](#10-adding-a-new-git-remote-and-checking-out-an-existing-feature-branch)
11. [Long-Living Branches vs. Short-Living Branches](#11-long-living-branches-vs-short-living-branches)
12. [Using GitLab Issues with Commits, Pipelines, and Merge Requests](#12-using-gitlab-issues-with-commits-pipelines-and-merge-requests)

---

## 1. Working Tree and Local vs. Remote Changes

- **Working Tree:** The working tree, also known as the working directory, is the directory on your local machine where you are currently modifying and adding files. It represents the state of your project's files at a specific point in time.

- **Local Changes:** Local changes are the modifications made to your files in the working tree that have not been committed yet. You can view the status of local changes by using the `git status` command. It provides information about which files have been modified, added, or deleted since the last commit.

- **Remote Changes:** Remote changes refer to the modifications made by others in the remote repository. These changes may include commits pushed by collaborators. To incorporate remote changes into your local repository, you can use commands like `git fetch` to retrieve the latest commits from the remote repository, followed by `git merge` to merge those changes into your local branch.

## 2. Setting VSCode as the Core Editor

To set Visual Studio Code (VSCode) as the default editor for Git commit messages, follow these steps:

1. Open a terminal or command prompt.

2. Execute the following command:
   ```
   git config --global core.editor "code --wait"
   ```
   This sets VSCode as the core editor for Git and ensures that Git waits for you to close the editor before proceeding with the commit message.

## 3. Restoring a File to its Last Commit

To discard local changes and restore a file to its last committed state, you can use the `git restore` command:
```
git restore <file-name>
```
This command replaces the file with the version from the last commit, effectively discarding any local modifications.

## 4. Git Status

The `git status` command displays the current state of your working tree and provides information about:

- Which files have been modified, added, or deleted.
- Files that are staged for commit.
- Branch information, including the current branch.
- Untracked files that are not yet added to Git.

Use `git status` to get a quick overview of the changes in your repository and the status of your files.

## 5. Restoring a Deleted File

If you have accidentally deleted a file in your working tree and want to restore it, you can use the `git restore` command with the `--source` option:
```
git restore --source <deleted-file>
```
Replace the `<commit-hash>` with the hash of the commit where the file was last present. This command restores the deleted file to its state at the specified commit.

## 6. Returning to a Previous Revision

To return to a previous revision, you can use the `git reset` command. It allows you to move the branch pointer to a specific commit and potentially modify the working tree.

- **Hard Reset:** Use `git reset --hard <commit-hash>` to move the branch pointer to the specified commit, discarding all changes in the working tree and index. This resets the repository to the state of the specified commit.

- **Mixed Reset:** Use `git reset --mixed <commit-hash>` to move the branch pointer to the specified commit, preserving the changes in the working tree but unstaging them. This allows you to review the changes before committing them again.

## 7. Restoring a Single File

To restore a single file to a specific version without affecting other files, you can use the `git restore --source` command:
```
git restore --source <commit-hash> <file-name>
```
Replace `<commit-hash>` with the hash of the commit that contains the desired version of the file, and `<file-name>` with the name of the file you want to restore. This command retrieves the specified file from the specified commit and updates it in your working tree.

## 8. Explaining the Reflog

The reflog, short for reference log, is a log that records changes to the branch references in your Git repository. It stores a history of all branch updates, including commits, branch creations, deletions, and rebases. The reflog is useful for recovering lost commits, undoing changes, or navigating the history of branch movements.

You can use the `git reflog` command to view the reflog and see a chronological list of reference updates. Each entry in the reflog contains information such as the commit hash, the action performed, the branch affected, and the commit message.

## 9. Explaining Rebasing

Rebasing is the process of integrating changes from one branch onto another by moving or combining commits. It allows you to incorporate the latest changes from a source branch into a target branch, resulting in a linear commit history.

The `git rebase` command is used to perform rebasing. It takes the commits from the source branch, removes them from their original location, and replays them onto the target branch. This process updates the commit history, making it appear as if the changes were made directly on the target branch.

Rebasing is commonly used to incorporate changes from a long-lived branch (e.g., `master`) into a feature branch before merging it back. It helps to keep the commit history clean and avoids unnecessary merge commits.

## 10. Adding a New Git Remote and Checking Out an Existing Feature Branch

1. **Add a new Git remote:**

   - Open a terminal or command prompt.
   - Navigate to the root directory of your local Git repository.
   - Use the following command to add a new remote:
     ```
     git remote add <remote-name> <remote-url>
     ```
     Replace `<remote-name>` with a suitable name for the remote, such as `origin` or `upstream`, and `<remote-url>` with the URL of the remote repository you want to add.

2. **Fetch the remote branches:**

   - After adding the remote, fetch the latest information about its branches using the command:
     ```
     git fetch <remote-name>
     ```
     This retrieves the branch references from the remote repository.

3. **Checkout an existing featurebranch:

   - Use the `git branch` command to view the available branches:
     ```
     git branch -a
     ```
     This lists both local and remote branches.

   - Identify the feature branch you want to checkout from the remote.

   - Create a local tracking branch based on the remote feature branch:
     ```
     git checkout -b <local-branch-name> <remote-name>/<remote-branch-name>
     ```
     Replace `<local-branch-name>` with a suitable name for your local branch and `<remote-name>/<remote-branch-name>` with the name of the remote branch you want to checkout.

     For example, if the remote branch is named `feature/xyz` and you want to create a local branch called `xyz`, the command would be:
     ```
     git checkout -b xyz origin/feature/xyz
     ```

   - You have now checked out the existing feature branch as a local branch. You can start working on it, make modifications, and commit your changes.

Remember to regularly fetch updates from the remote repository to stay in sync with any changes made to the feature branch by other collaborators. You can use the `git fetch <remote-name>` command to fetch the latest changes.

## 11. Long-Living Branches vs. Short-Living Branches

- **Long-Living Branches:** Long-living branches, often referred to as main branches or master branches, represent stable, production-ready code. They are intended to be persistent and serve as the primary branches for ongoing development and releases.

- **Short-Living Branches:** Short-living branches, such as feature branches or bug fix branches, are created for specific tasks or features and have a limited lifespan. They are used for isolated development, allowing changes to be made without affecting the stability of long-living branches. Once the task or feature is completed, short-living branches are typically merged into the main branch and closed.

## 12. Using GitLab Issues with Commits, Pipelines, and Merge Requests

GitLab provides an issue tracking system integrated with Git. You can link your commits, pipelines, and merge requests to GitLab issues for better visibility and organization.

To link a commit to an issue, include the issue reference in the commit message using the syntax `#<issue-number>`. For example:
```
git commit -m "Implemented feature XYZ (#123)"
```
This associates the commit with the issue and creates a link between them.

To link a pipeline to an issue, you can use GitLab CI/CD configuration files, specifying the issue reference in the pipeline definition.

To link a merge request to an issue, create a merge request and mention the issue in the description or comments using the syntax `Closes #<issue-number>`. This automatically closes the issue when the merge request is accepted.

To make a merge request and squash commits in GitLab, follow these steps:

1. Push your branch: Before creating a merge request, ensure that your branch with the desired changes is pushed to the remote repository. Use the command:
   ```
   git push origin <branch-name>
   ```

2. Navigate to GitLab: Open your web browser and go to the GitLab repository where you want to create the merge request.

3. Create a merge request:
   - Click on the "Merge Request" tab or button.
   - Choose the source branch (the branch with your changes) and the target branch (the branch you want to merge into).
   - Provide a title and description for the merge request, explaining the changes you made.

4. Squash commits:
   - In the merge request view, locate the "Squash commits" option.
   - Enable the option to squash your commits into a single commit.

5. Optionally, edit the commit message that will summarize all the squashed changes.

6. Review and submit:
   - Review the changes, diff, and commit message to ensure everything is correct.
   - Add any additional reviewers or assignees, if necessary.
   - Click on the "Submit merge request" or similar button to create the merge request.

GitLab will now process the merge request and provide a summary of the changes. The squashed commits will be merged into the target branch as a single commit, improving the clarity and cleanliness of the commit history.

Remember to regularly check the status of your merge request, address any comments or feedback, and follow any specific guidelines or processes set by your team or project.

#### WIP
### Reverting a Git Commit

To revert a Git commit means to create a new commit that undoes the changes made in a previous commit. This allows you to effectively remove the changes introduced by a commit without modifying the commit history.

To revert a Git commit, you can follow these steps:

1. Identify the commit to revert: Use `git log` to view the commit history and find the commit you want to revert. Take note of the commit hash or the commit reference.

2. Revert the commit: Execute the following command, replacing `<commit-hash>` with the hash of the commit you want to revert:
   ```
   git revert <commit-hash>
   ```
   This command creates a new commit that undoes the changes made in the specified commit. Git uses an automatic merge process to apply the inverse changes.

3. Add a revert commit message: When you execute the `git revert` command, Git opens your default text editor for you to enter a commit message. Provide a descriptive message explaining the reason for the revert.

4. Save and close the commit message: Save the commit message and close the text editor. Git will create the revert commit with the provided message.

5. Push the changes (if necessary): If you want to share the revert commit with others, use `git push` to push the changes to the remote repository:
   ```
   git push origin <branch-name>
   ```
   Replace `<branch-name>` with the name of the branch where the reverted commit was made.

### How Revert Works

When you revert a commit, Git analyzes the changes introduced by the commit and creates a new commit that undoes those changes. It accomplishes this by applying the inverse changes to the codebase.

Git achieves the revert by performing the following steps:

1. Git identifies the commit to revert based on the commit hash or reference provided.

2. Git compares the changes introduced by the commit with the previous commit. It determines the differences between the two states of the codebase.

3. Git calculates the inverse changes required to undo the modifications introduced by the commit.

4. Git applies the inverse changes to the codebase, effectively undoing the modifications made by the commit.

5. Git creates a new commit with the reverted changes. This commit is separate from the original commit, preserving the commit history.

By creating a revert commit, Git allows you to safely undo changes without modifying the existing commits. This is particularly useful when you want to keep a clear and accurate history of the project while still addressing issues or reverting unwanted modifications.

### Git Commit History

In Git, the commit history represents the sequence of commits made to a repository over time. It provides a chronological record of changes, allowing you to track the evolution of the codebase and understand the development process. The commit history is an essential aspect of version control and collaboration in Git.

Each commit in the history consists of the following information:

- **Commit Hash:** A unique identifier for the commit, typically represented as a hexadecimal string. The commit hash serves as a reference to identify and access a specific commit.

- **Author and Timestamp:** The author of the commit, usually associated with a name and email address. It also includes the timestamp indicating when the commit was created.

- **Commit Message:** A descriptive message provided by the author, explaining the purpose or changes introduced by the commit. A good commit message is concise, meaningful, and helps others understand the context of the changes.

- **Parent Commits:** Commits can have one or more parent commits, indicating the commit(s) from which the changes originated. In most cases, a commit has a single parent, forming a linear sequence of commits. However, in cases of branching or merging, a commit can have multiple parents, representing the merge of different branches.

- **Changes:** Each commit represents a set of changes made to the codebase. These changes can include additions, modifications, or deletions of files and directories. The commit captures a snapshot of the codebase at the time of the commit.

The commit history can be visualized as a directed acyclic graph (DAG), where each commit is a node connected to its parent commit(s). The graph illustrates the branching and merging of code changes, allowing you to visualize the relationships between different commits and branches.
