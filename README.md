# Git Notes

Learning Git from Primeagen on [YouTube](https://www.youtube.com/watch?v=rH3zE7VlIMs&t=62s)

## Part 1: Using Git Solo

### Installing and Configuring Git

Install Git on Mac:
```
brew install git
```

Check the name and email that is currently set:

```
git config --get user.name
```

```
git config --get user.email
```

To set the name and email, use the following commands:

Note: This data is stored in a single file (`.gitconfig`):
    - Local: The `.git` directory in the current directory that has git initialized
    - Global: The home directory

```
git config --add --global user.name "username"
```

```
git config --add --global user.email "email"
```

To set the default branch globally, use the following command

```
git config --add --global init.defaultBranch master
```

### Porcelain and Plumbing Commands

```
Porcelain: High-level commands in Git

Examples:
    git status
    git add
    git commit
    git push
    git pull
    git log
```

```
Plumbing: Low-level commands in Git

Examples:
    git apply
    git commit-tree
    git hash-object
```

### Git Repositories

Git takes a snapshot of the entire project state each time a commit is made. It doesn't only store the changes made at each step, but the entire snapshot of the project.

Git is made up of objects stored in the `.git/objects` directory.

Each commit is stored in the `.git` directory, but catting the file will not allow you to read it since the file is compressed into bytes (the main reason why git is so small).

#### Status

There are several states for each file in a git repo

Examples:  
    - `untracked`: Not being tracked by git  
    - `staged`: Marked for inclusion in the next commit  
    - `committed`: Saved to the repo's history

#### Staging

After we create/edit files, we need to add them to the staging area

To do so, use the following command:

```
git add <filename>
```

We can also use:

Note: if you are not in the root directory of the project, it will only add all of the contents in the current directory and its parent directories and files

```
git add .
```

#### Commits

After adding the files to the staging area, we need to make a commit. Typically, we will add a message with the commit to describe what changes we made

To commit the changes, use the following command:

```
git commit -m "your message here"
```

#### Logs

After committing, we can inspect the history of commits for the project  
To view the logs, use the following command:  
Note: This command will output the last 10 commits

```
git --no-paper log -n 10
```

There are also other options that we can add to the end of the command to change the viewing of the logs.

Examples:  
    - `--oneline`: Outputs each commit as a single line  
    - `--parents`: Adds annotations for the parent commits  
    - `--graph`: Displays the graph of commits, and its being merged back in 

#### Cat File

Note: Remember that each commit is an object that is compressed to bytes in git.

If we want to view the commit contents, we can use the built in plumbing command to view the contents of git. To view the changes, use the following command:

```
git cat-file -p <hash>
```

Important to understand:  
    - `tree`: directory  
    - `blob`: file 

Steps to take:

1. Find the commit you want to inspect and get its hash (use the `git log` command)

2. Use the `git cat-file` command to find the directory hash (the hash after the keyword `tree`)

3. Use the `git cat-file` command to find the file hash (the hash after the keyword `blob`)

4. Use the `git cat-file` command to cat the contents of the file using the hash from the previous step

### Inspecting Git History

### Branching

### Merging

### Rebasing

### Undoing Changes

### Remote Repos and GitHub

## Part 2: Using Git in a Team