# Gitflow Workflow

## What is Git?

Git is a version control system that tracks versions of files. It is used to control source code written by programmers who develop software collaboratively.

Source code resides in what Git refers to as a repository, which can be hosted on platforms like GitHub. Every user working with a Git repository has a complete copy of the repository on their machine, including the full history of all changes, on their local machine.

An example of a highly relevant Git repository is shown below:

[https://github.com/qkrt-rm/qkrt-mcb](https://github.com/qkrt-rm/qkrt-mcb)

This is the Drive Control project’s Git repository. By the end of this meeting, you will understand how to create a copy of any remote repository and contribute to it in a collabrative setting.

---

## The Gitflow Workflow Branching Model

Before moving on, open a terminal and change your working directory to some project folder on your system using the `cd` terminal command. Then clone our `git-sandbox` repository which we will use to learn and practice this workflow. The commands to do this are shown below:

```bash
cd some/project/directory
git clone https://github.com/qkrt-rm/git-sandbox.git
cd git-sandbox
```

The goal of the Gitflow Workflow is to balance simplicity with collaboration, providing a structured branching model:

- **Main Branches**:
    - **Main (or Master)**: Contains the production-ready code.
    - **Develop**: Serves as the integration branch for development.
- **Supporting Branches**:
    - **Feature Branches**: Created from `develop` for new features. Merged back into `develop` once completed.
    - **Release Branches**: Created from `develop` when preparing a new release. Used for final testing and bug fixes before merging into both `main` and `develop`.
    - **Hotfix Branches**: Created from `main` to address critical issues. Merged back into both `main` and `develop`.
- **Workflow**:
    - Developers create feature branches for individual tasks.
        1. Create a feature branch using the develop branch as your starting point. The name of a feature branch must have the prefix `feature/` followed by the name of the feature:
            
            ```bash
            git switch -c feature/omni-drive develop
            ```
            
        2. Work on the feature:
            
            ```bash
            touch omni_drive.py  # implement feature (or part of feature)
            git add -A  # add changes
            git commit -m "implemented part of omni-drive"  # commit changes
            ```
            
        3. Push your changes as you work on the feature:
            
            ```bash
            # you only need to include '-u <repository> <branch>' the first time
            git push -u origin feature/omni-drive
            
            # after the first time, you can simply call 'git pull' or 'git push'
            git push
            ```
            
    - Changes are merged into `develop` via pull requests, ensuring code review and testing.
        1. Use Github to create a pull request from `feature/new-feature` into `develop`.
        2. Delete the branch both locally and on the remote repository (GitHub might prompt you to delete the branch which is also fine).
            
            ```bash
            git branch -d feature/new-feature
            git push origin --delete feature/new-feature
            ```
            
    - When a release is ready, a `release` branch is created for finalization.
        1. Create the release branch. The name of a release branch must have the prefix `release/` followed by the version of the next release:
            
            ```bash
            git switch -c release/1.0.0 develop
            ```
            
        2. Run tests and then commit and push final changes:
            
            ```bash
            git add .  # add fixes
            git commit -m "fix bugs for release v1.0.0"  # commit fixes
            git push origin release/1.0.0
            ```
            
        3. Merge into both `main` and `develop` branches:
            
            ```bash
            # Merge into main
            git checkout main
            git merge --no-ff release/1.0.0
            git tag -a v1.0.0 -m "Release version 1.0.0"
            
            # Merge into develop
            git checkout develop
            git merge --no-ff release/1.0.0
            
            ```
            
        
        Delete the release branch:
        
        ```bash
        git branch -d release/1.0.0
        git push origin --delete release/1.0.0
        ```
        
    - Emergency fixes go through `hotfix` branches to quickly patch production.
        
        ```bash
        git switch -c hotfix/critical-fix main
        ```
        
        ```bash
        # Commit changes
        git add .
        git commit -m "fix critical bug in production"
        ```
        
        ```bash
        # Merge into main
        git checkout main
        git merge --no-ff hotfix/critical-fix
        git tag -a v1.0.1 -m "Hotfix version 1.0.1"
        
        # Merge into develop
        git checkout develop
        git merge --no-ff hotfix/critical-fix
        
        ```
        
        ```bash
        git branch -d hotfix/critical-fix
        git push origin --delete hotfix/critical-fix
        ```
        

This approach ensures clear organization, supports parallel work, and minimizes conflicts.

---

## Cloning our Project Repository

If you take a look at the front page of our repository on GitHub, you’ll see what looks like links to other repositories. Those links are Git submodules which are essentially just repositories that were added to the main repository.

![image.png](Gitflow%20Workflow/image.png)

If you plan to clone a working project, these Git submodules need to be individually cloned as well, just like any other repository. To correctly clone our project repository, as well as all of its submodules, do the following:

1.  Click the green “Code” button and copy the HTTPS URL to your clipboard like below:
    
    ![image.png](Gitflow%20Workflow/image%201.png)
    
2. Open a terminal and change your directory to some project directory using the `cd` terminal command.
    
    ```bash
    cd some/project/directory
    ```
    
    You can also use the `mkdir` command to create directories that don’t already exist.
    
    ```bash
    mkdir ~/dev  # creates a directory called 'dev' in the home directory
    ```
    
3. Use the `git clone` command making sure to include the `--recursive` option to recursively clone the submodules as well.
    
    ```bash
    git clone --recursive https://github.com/qkrt-rm/qkrt-mcb.git
    ```
    

## Handling Merge Conflicts

---

## Important Git Commands to Know

- `git clone [<options>] <repository> [<directory>]`
    
    > Create a local copy of a remote repository, including all its branches, commits, and files.
    > 
    > - `[<options>]`
    >     - `--recursive` or `—recurse-submodules[=<pathspec>]`
    >         
    >         > After the clone is created, initialize and clone submodules within based on the provided `<pathspec>`. If no `=<pathspec>` is provided, all submodules are initialized and cloned.
    >         > 
    >     - `-b <branch>` or `--branch <branch>`
    >         
    >         > Clone a specific `<branch>` of `<repository>`
    >         > 
    > - `<repository>`
    >     
    >     > is the URL or path of the repository to clone
    >     > 
    > - `[<directory>]`
    >     
    >     specifies the name of the local directory where the repository will be cloned. If omitted, the directory defaults to the repository's name.
    >     

- `git add [<options>] [<pathspec>...]`
    
    > Add file contents to the index. The index in Git is a staging area where changes are prepared before committing. It holds a snapshot of your working directory that you want to include in the next commit.
    > 
    > - `[<options>]`
    >     - `-f` or `--force`
    >         
    >         > Allow adding otherwise ignored files.
    >         > 
    >     - `-A` or `--all`
    >         
    >         > Stages changes (new, modified, deleted files) globally, across the entire repository.
    >         > 
    > - `[<pathspec>...]`
    >     
    >     > Specifies the files or directories to stage. If omitted, Git stages all changes (modified, deleted, and untracked files) in the current directory and its subdirectories.
    >     > 

- `git rm [<options>] <pathspec>...`
    
    > Remove files from the working tree and from the index.
    > 
    > - `[<options>]`
    >     - `-f` or `--force`
    >         
    >         > Forces removal of files that have changes or are already staged for commit.
    >         > 
    >     - `--cached`
    >         
    >         > Removes files from the staging area (index) without deleting them from the working tree.
    >         > 
    >     - `-r`
    >         
    >         > Allows recursive removal of files in directories.
    >         > 
    > - `<pathspec>...`
    >     
    >     > Specifies the files or directories to remove from .
    >     > 

- `git commit [<options>] [<pathspec>...]`
    
    > Record staged changes in the repository's history, creating a new commit with a message describing the changes.
    > 
    > - `[<options>]`
    >     - `-m <msg>` or `--message=<msg>`
    >         
    >         > Use the given `<msg>` as the commit message. If multiple `-m` options are given, their values are concatenated as separate paragraphs.
    >         > 
    >     - `--amend`
    >         
    >         > Modify the most recent commit. Can be used with `--no-edit` to avoid opening the commit message editor
    >         > 
    > - `[<pathspec>...]`
    >     
    >     > Specifies which files or directories to include in the commit. If omitted, Git will commit all staged changes.
    >     > 

- `git pull [<options>] [<repository> [<refspec>...]]`
    
    > Fetch changes from a remote repository and integrates them into your current branch. It combines two commands: `git fetch` (to download changes) and `git merge` (to integrate them).
    > 
    > - `[<options>]`
    >     - `-r` or `--rebase`
    >         
    >         > Rebase your local changes on top of the fetched changes instead of merging them.
    >         > 
    >     - `-u` or `--set-upstream`
    >         
    >         > Associate your current branch with a remote tracking branch, so you don’t need to explicitly specify the branch for future commands like `git pull` or `git push`.
    >         > 
    > - `[<repository> [<refspec>...]]`
    >     
    >     > `<repository>` is the name of the remote repository to pull from (e.g., `origin`). If omitted, Git uses the default remote (usually `origin`).
    >     > 
    >     > 
    >     > `[<refspec>...]` specifies which branch(es) or tag(s) to pull from. If omitted, Git pulls from its upstream branch.
    >     > 

- `git push [<options>] [<repository>] [<refspec>...]`
    
    > Upload commits from your local repository to a remote repository, allowing others to access your changes. It typically pushes the current branch to its remote counterpart, updating the remote with your latest work.
    > 
    > - `[<options>]`
    >     - `-f` or `--force`
    >         
    >         > Force-push changes, overwriting the remote history.
    >         > 
    >     - `-u` or `--set-upstream`
    >         
    >         > Associate your current branch with a remote tracking branch, so you don’t need to explicitly specify the branch for future commands like `git pull` or `git push`.
    >         > 
    > - `[<repository>]`
    >     
    >     > The name of the remote repository to push to (e.g., `origin`). If omitted, Git uses the default remote (usually `origin`).
    >     > 
    > - `[<refspec>...]`
    >     
    >     Specifies which branches or tags to push. If omitted, Git pushes the current branch to its upstream branch. You can also use the `--delete` option to instead delete all listed refs from the remote repository.
    >     

- `git fetch [<options>] [<repository> [<refspec>...]]`
    
    > Retrieves updates from a remote repository without modifying your local working directory or branches. It downloads, new commits, branch updates, and tags or other references.
    > 
    > - `[<options>]`
    >     - `-f` or `--force`
    > - `[<repository> [<refspec>...]]`
    >     
    >     

- `git switch [<options>] <branch>`
    
    > Switch the current branch to `<branch>`.
    > 
    
    `git switch [<options>] (-c|--create) <new-branch> [<start-point>]`,
    
    > Create a new branch called `<new-branch>` and switch to it.
    > 
    > - `[<start-point>]`
    >     
    >     > The commit or branch from which the new branch will start. Can be a branch name, commit hash, or tag. If omitted,
    >     > 
    
    `git switch [<options>] (-d|--detach) [<start-point>]`
    
    > Switch to a branch or commit for inspection and discardable experiments. If it turns out whatever you have done is worth keeping, you can create a new branch for it (without switching away) by executing: `git switch -c <new-branch>`.
    > 
    > - `[<start-point>]`
    >     
    >     > The commit or branch from which the detached environment will start. Can be a branch name, commit hash, or tag.
    >     > 
    
    `git switch [<options>] —orphan <new-branch>`
    
    > Switch to a branch without any commit history, effectively creating an empty branch.
    > 

- `git restore [<options>] <pathspec>...`
    
    > Revert the file to the last committed state, removing any modifications in your working directory
    > 
    > - `<pathspec>...`
    >     
    >     > Specifies which files or directories to revert.
    >     > 
    
    `git restore [<options>] --source=<commit-hash> <pathspec>...` 
    
    > Revert a file in your working directory to its version from a specific commit.
    > 
    > - `<pathspec>...`
    >     
    >     > Specifies which files or directories to revert.
    >     > 
    
    `git restore --staged <pathspec>...`
    
    > Remove a file from the staging area, but keep its changes in the working directory.
    > 
    > - `<pathspec>...`
    >     
    >     > Specifies which files or directories to remove from the staging area.
    >     > 

- `git branch [<options>]`
    
    > List all branches.
    > 
    > - `[<options>]`
    >     - `-a`
    >         
    >         > Include remote branches.
    >         > 
    >     - `-v`
    >         
    >         > Verbosely list all branches; Show sha1 and commit subject line for each head, along with relationship to upstream branch (if any).
    >         > 
    
    `git branch <new-branch> [<start-point>]`
    
    > Create a new branch called `<new-branch>` without switching to it.
    > 
    > - `[<start-point>]`
    >     
    >     > The commit or branch from which the new branch will start. Can be a branch name, commit hash, or tag.
    >     > 
    
    `git branch -m <new-branch>`
    
    > Rename the current branch to `<new-branch>`. You can use `-M` instead of `-m` which is shorthand for `-m --force` and will overwrite existing branches of the same name.
    > 
    
    `git branch (-d | --delete) <branch>`
    
    > Locally delete `<branch>`.
    > 
    
- `git remote [-v | --verbose]`
    
    > List the set of repositories (”remotes”) whose branches you track. Include `-v` to also show remote url after name.
    > 
    
    `git remote add [<options>] <name> <URL>`
    
    > Add a remote named `<name>` for the repository at `<URL>`. The command `git fetch <name>` can then be used to create/update remote-tracking branch `<name>/<branch>`.
    > 
    > - `[<options>]`
    >     
    >     
    
    `git remote remove <name>`
    
    > Removes remote named `<name>` from the list of added remotes.
    > 
    
    `git remote rename <old> <new>`
    
    > Renames remote named `<old>` to `<new>`.
    >

# Contributions
* Initial Guide made by Hunter Cocker.