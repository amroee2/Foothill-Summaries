# Git and Github

Git is a Version Control System designed to:

- Record changes made to a file overtime.
- Ability to revert back to a previous file version or project version.
- Compare changes made from one version to another.
- Version control on text files, not just source code.

## The 3 Stages of File

![image](https://github.com/user-attachments/assets/8115cf5f-e998-4f5c-862a-83145b4fc3f0)

## The 3 Stages of a Git Project

![image](https://github.com/user-attachments/assets/3233067b-eae3-4a7e-bb9b-812980654b5d)

## Initializing a git repo and connecting it to Github

1. Cd to the directory.
2. Git init command.
3. Stage (git add) and commit (git commit with -m for message) to add to staging area then commiting to local repo.
4. Set the github remote remote using git remote add origin (link).
5. Push changes to remote repo (Github repo) using git push -u origin master.

# Common Git commands 

## Git Status 

Git status is used to see which stages is each file in and checks if its up to date with origin/master (Branches discussed later)

![image](https://github.com/user-attachments/assets/a392ec04-206d-4f5f-b13e-a8bf60ee0ba1)

### No changes/Up to date
![image](https://github.com/user-attachments/assets/94c9bb52-5d94-4774-90d4-28b0268488a9)

### New file
New files created are called **Untracked files**, they become tracked once they are added into the staging area

![image](https://github.com/user-attachments/assets/428957c1-ef9d-4bc5-8468-33a06baaf5d6)

### Staged but not comitted files

![image](https://github.com/user-attachments/assets/e73fb288-96fb-41d1-a88c-853138275342)

### Files in multiple stages

After editing a file that was already staged, the file will be in 2 sections, modified files and changed to be comitted files.

![image](https://github.com/user-attachments/assets/821c801c-890c-4d0f-b741-f157cbe97306)

## Git Status --short

Works the same as Git status, but it gives a short description of the status like this:

![image](https://github.com/user-attachments/assets/8acff0c1-7dde-4910-9dd8-e2e51f38405e)

Where the letters indicate which stage the file is in like this:

![image](https://github.com/user-attachments/assets/d4af6f76-1687-4c58-8bd8-069a6c3ba9ed)

- First row indicates a file modified and staged.
- Second row indicates a file modified and staged but was modified again in the working directory.
- Third row indicates a new file added into the staging area.
- Fourth row indicates untracked files.

### Example comparison 

Git status

![image](https://github.com/user-attachments/assets/9f643b51-84b5-4cb9-81fb-496942713117)

--short

![image](https://github.com/user-attachments/assets/ffa798cc-2b25-4e27-b30e-d0a6bbe1c42b)

## Git Diff

Git diff is communly used to check the difference between 2 versions of the same file/project, it answers 2 questions:

![image](https://github.com/user-attachments/assets/02d59745-526b-4c0c-af5d-e0bd0cacfe1f)

## Git diff --staged

First question is answered using GIt diff --staged, which compares the last commited snapshot with the currently staged files

![image](https://github.com/user-attachments/assets/fdd24863-4ee6-40e5-b205-4c15510c4891)

**How to read the output**

![image](https://github.com/user-attachments/assets/cfed8326-87de-436c-8b88-ed147351ee64)


- First line indicates the command.
- Second line indicates which files are being compared.
- File Metadata is like a code for the files, first 2 numbers is a hash for the files, more advanced for now.
- Markers indicate which file is being represented, in this example the minus represents a/file1.txt and the plus represents b/file1.txt
- Chunk header indicates the changes, in this example, it says that the file begins at line 12 and it has 2 lines added for a/file1, while its 3 for b/file1
- Finally it shows the exact difference in lines.

### Example

![image](https://github.com/user-attachments/assets/e5dbae9d-1e07-4159-b058-3ba1e44a1030)

Newfile.txt is a file that was newly created, as such the last commit does not contain it, so it indicates that its a new file with the Metadata 000000 since the last commit doesnt have it, there is no hash reference.

## Git diff

It shows the difference between the staged files and the files in the working directory.

![image](https://github.com/user-attachments/assets/f76e0c1c-b177-4bda-b71c-95d2614ca6a0)

![image](https://github.com/user-attachments/assets/edfa385f-2703-4b79-a9a6-be95050f743d)


newfile.txt was empty at the beginning then staged, and then modified as it can be seen in the git status command output, so the difference is shows in git diff, but not in git diff --staged

![image](https://github.com/user-attachments/assets/98cd6c1f-ca52-4944-a220-3ca3a8648d08)

## Commit without having to stage files

Used only in very small projects, can be done using git commit **-a** -m (commit message).

# More Git Commands

## Git log

Git log is used to see the previous commits to the local repo:

![image](https://github.com/user-attachments/assets/68dea024-ef4a-493b-862b-f51ccfa9140e)

### --oneline

Provides a much shorter description for the commits 

![image](https://github.com/user-attachments/assets/e2f6d50f-4a04-4cca-aa7e-b5b851c37713)

### --stat

Provides statistics (number of files changed)

![image](https://github.com/user-attachments/assets/b7a32e98-9bbd-41f4-89a1-edf67328edfb)

### --patch

Same as git -diff, but between 2 commit snapshots

![image](https://github.com/user-attachments/assets/f8207d20-d770-410d-af63-db6b71179269)

## Remove and rename files

## Remove files

### git rm

![image](https://github.com/user-attachments/assets/7cc80c39-1bbb-4d51-8808-b1a61746eac3)

### git rm --cached

It's also possible to cache the files instead of completely remove them from directory

![image](https://github.com/user-attachments/assets/f695eb22-bbb4-4813-af47-4adc5cfe0fe7)

(employee.txt) is still in the directory even after being removed

## Rename files

### git mv
File renamed coflict.txt -> conflict.txt
![image](https://github.com/user-attachments/assets/99171b64-7a77-4b39-844f-834227a4a1b1)

# Introduction to Branches

Git branches are essentially pointers to snapshots of your changes in a Git repository. They help you manage different lines of development and isolate features, fixes, or experiments from the main codebase.

## git checkout -b

To create a new branch, we use git checkout -b (branch  name):

![image](https://github.com/user-attachments/assets/c836dc10-7e25-4611-99b9-ee0a7541633b)

The new branch will have the same git status and the files as the previous one:

![image](https://github.com/user-attachments/assets/a7577da3-e6e0-4077-8a24-c2a0cabaf234)

To switch to a specific branch, we use git checkout (branch name):

![image](https://github.com/user-attachments/assets/cbe2e31d-2563-4f81-afda-ea8f5e9c727f)

## Typical issue with branches

When working on and modifying files in a branch, we must keep into account the file content in the other branch to avoid overwriting, example of such conflict:

![image](https://github.com/user-attachments/assets/94f0b7b3-076b-405f-8a01-7969219137e0)

Here, in a branch called thirdBranch, "anotherfile.txt" was cached and then the changes were comitted, and when switching back to the master branch, error happens:

![image](https://github.com/user-attachments/assets/1a5b146b-d423-4080-8438-b5dfdcf6dc08)

## Git stash

One of the ways to fix the error is by using git stash after adding into the staging area, it acts as if changes were comitted, and the WIP (work in progress) is stored in the "stash", previous stashes can also be accessed through stash list.

![image](https://github.com/user-attachments/assets/27159af2-e0fa-4415-bb78-1de945336dc9)

## Merging Branches

Branches can be merged through **git merge (branch name)**, like this:

![image](https://github.com/user-attachments/assets/1d417b41-9dbd-4e01-bba8-450187aa7e48)

After branches are merged, it acts as if its a commit, and when merging more branches it creates a new commit, resulting in increase in the number of commits ahead of the origin/master:

![image](https://github.com/user-attachments/assets/0d422f6d-ddd9-4d7b-a6cd-2416ed1d41d5)

Through git log, we can find the commits ahead of the origin/master branch:

![image](https://github.com/user-attachments/assets/9940b623-2d38-468f-805f-5598bcf5d45f)

# Resets 

Rests are used to rollback a commit, which is a dangerous process, there are 3 types of reset:

![image](https://github.com/user-attachments/assets/15aebcff-c3b6-42f3-a817-2a8247d868df)

We can use reset --mixed to reset the 5 commits into the working stage, which would make it look like this:

![image](https://github.com/user-attachments/assets/9b98e6e7-5073-4d67-9c21-25295f44c112)

Then we can add all files and commit them again, basically grouping the 5 commits into 1, and pushing everything

![image](https://github.com/user-attachments/assets/cb2fdc96-d93b-461a-bcfa-0c3e1ff8f49a)

# Commit messages

Commit messages are very important when working with git, as it provides a clear description for the user and the team partners, there are 7 rules that must be followed when writing a commit message, which can be accessed through [here](http://chris.beams.io/posts/git-commit)

# Playing with git 

Another useful link to practice [git commands](http://git-school.github.io/visualizing-git)
