# Git for Professionals

# The Perfect Commit

Commits are important in git as they indicate what version of the project we are working on, so there are 2 main points that help make the perfect commit.

## Seperate changes 

Making multiple changes across multiple files and cramping them in one commit can cause confusion and makes it harder to track changes. Its best to "divide" commits into multiple smaller ones to avoid this issue.

![image](https://github.com/user-attachments/assets/c7d50e36-4233-4d6b-b32c-06cb19fc1016)

We could also commit a file and only a **part** of another file.

Suppose we have this recipe for a chocolate bar, and we decide to make some changes.
![image](https://github.com/user-attachments/assets/342453b8-db5a-4fe2-acf7-1c21fd82dc98)

And through **git diff** to compare the list commit and the working directory, we can see the changes we made.

![image](https://github.com/user-attachments/assets/d7b8b388-0a91-4c9f-9413-e559364d6a2b)

Through **git add -p (file name)** we can choose which hunk (part of code in different contexts) do we want to commit and which ones we want to keep. Here since this is a simple recipe file, we only have one hunk, we can choose to add it through y for yes or n for no.
![image](https://github.com/user-attachments/assets/387b7c98-8ed2-49cd-ad1b-c043f3d57b13)

![image](https://github.com/user-attachments/assets/617230c2-3771-418a-accd-668ffa3284a7)

## Perfect Commit Message

![image](https://github.com/user-attachments/assets/1a840cbd-8b37-4a95-9342-8ab53cb86ed1)

Suppose we decide to update the description to make it less complicated.

![image](https://github.com/user-attachments/assets/5e2ebac8-897f-45e6-b1e8-8dbe9fbd7f55)

A good commit message might look like this (ignoring the Lines "starting" line), git knows to differeniate the subject and the body when we add an empty line between the two.

![image](https://github.com/user-attachments/assets/dae81516-619a-4c5f-974d-f6fc8ac73005)

# Branching Strategies 

Branching stratigies refer to the ways you and your team want to handle branches, its like a convention that everyone follows.

![image](https://github.com/user-attachments/assets/8c6a6964-2182-4bd0-ac42-b2e60aacf99b)

## Mainline development "Always Be Integrating"

Its an ideal workflow and hardly ever exists in the real world, team only has few branches, small commits to main branch and high quality testing & QA.

![image](https://github.com/user-attachments/assets/fceceb10-f643-4b66-a171-9f5cb69958c1)

## State, Release and Feature Branches

Each branch fulfill differnt types of jobs, then these changes can be merged into main.

![image](https://github.com/user-attachments/assets/15d15038-0177-4ecf-84a4-252639eae717)

**Long Running Branches**: Long living branches are branches like main or master in repos that stay for a long time and integrated into.

**Short Lived Branches**: Branches that don't stay for long, for new features, bug fixes, refactoring or expirements, will most likely be deleted after integration (merge/rebase).

## Github flow Strategy

Very simply, one one long running branch (main/master) and short living branches for features.

**Commits are to not be directly into main, but merged into it**
![image](https://github.com/user-attachments/assets/9488a13c-021b-4145-98ae-d496b62c77b8)

## GitFlow Strategy 

2 long running branches, main/master and a develop branch, where changes from short living branches are merged into develop branch and then from there they are merged into main.

![image](https://github.com/user-attachments/assets/38efc441-33a9-4219-bcf5-84b08440d63b)

# Pull Requests

Pull requests are in short requests to merge a branch into main, its like another layer of safety before merging into main in the remote repository on Github or any place where git is hosted.

These are changes that i added into pull.txt and would like to merge into main.

![image](https://github.com/user-attachments/assets/4a51bf37-5e76-46e0-a608-15a039d26d42)

We can add a subject and and description here and send the request for review and reviewers can decide if we should merge or not

![image](https://github.com/user-attachments/assets/d38452dd-0592-4ad4-9d3e-6004b1fb3944)

And from git we can pull the changes and see using git cat-file for the last commit that its a merged commit (2 parents).
![image](https://github.com/user-attachments/assets/34581211-2408-4521-a390-37c42fe703ea)
