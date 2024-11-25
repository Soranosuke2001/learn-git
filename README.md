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

#### Configuring Git Locally

Note: Git will allow you to have multiple key names that are the same in the config file

Sometimes, we want to store some information locally. Although its not safe, we can store information inside the `.git` folder since its hidden.

There are different location that we can store the config for git:  

Note: The overriding priority is in order (worktree has the highest priority)  
    - `system`: configures git for all users in the system (90%)  
    - `global`: configures git for all projects for the user (9%)  
    - `local`: configures git for a single project (1%)  
    - `worktree`: configures git for a part of a project

#### Adding to Git Config

Use the following command to store key/value pairs inside the git config file: `./.git/config`

Note: We can also put in a section by adding a `.`, before the key

```
git config --add --local <section>.<key> <value>
```

#### Viewing Git Config

To view the contents, we can use either of the commands below:

Note: Both will list all configs in the `./.git/config` file

```
git config --list --local
```

```
cat ./.git/config
```

To get a value from its key, we can use the following command

```
git config --get <section>.<key>
```

#### Removing Configs

To remove a key/value pair from the config, use the following command

Note: If there are more than one where the key is the same, nothing will happen and a warning is outputted

```
git config --unset <section>.<key>
```

To remove all key/value pairs with the same keyname, use the following command

```
git config --unset-all <section>.<key>
```

To remove an entire section (even when there are still key/value pairs), use the following command

```
git config --remove-section <section>
```

#### Updating Configs

To update a key/value pair from the config, use the following command

```
git config --set <section>.<key>
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

To view the changes made during the previous commits, use the following command:

```
git log -p
```

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

### Storing Data

Git stores the entire snapshot of the project at each commit made, which is saved to the `.git` directory. There are optimizations made in order to keep the directory small.

#### Optimizations

Storage optimizations:  
    - Git compresses and packs files to store them more efficiently  
    - Git deduplicates files that are the same across different commits (doesn't duplicate if no changes are made) 

Steps to take:

1. Create a commit with a sample file

2. Create another commit with a new sample file, but do not change the previous file

3. Check the hash for the file in the first commit and compare it to the hash from the second commit for the same file (use the `git cat-file` command)

Note: Notice that the hash for the file doesn't change, in other words, the file was not duplicated

### Inspecting Git History

### Branching

### Merging

### Rebasing

### Undoing Changes

### Remote Repos and GitHub

## Part 2: Using Git in a Team