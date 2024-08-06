# Branches

Most systems are large and complex and require multiple people working on the system, to maintain this workflow we can use branches.

## Create a new branch

Creating a new branch can done by **git chekout -b (branchname)**

![image](https://github.com/user-attachments/assets/fc611d6c-b559-4865-8f91-4d1755af194c)

To switch between branches, we use **git checkout** or **git switch**

![image](https://github.com/user-attachments/assets/e905a0be-b69d-4f02-baee-95895aa109a4)

## We can list all branches by using git branch

![image](https://github.com/user-attachments/assets/e29ab478-b141-4766-a43c-200edc4da4e3)


## Files in branches

When creating a new branch, the new branch will have the same files, but any new files created and worked on in the new branch will be only for it

![image](https://github.com/user-attachments/assets/2acc9b39-e497-46ef-8a11-b7ad72bddcfc)

## Rename and Delete branches

### Renaming

We can rename branches by using **git branch -m (old name) (new name)**

![image](https://github.com/user-attachments/assets/2e90cb54-b16e-4579-a672-654eb5bf5acf)

or if we want to rename the branch we are in, we can just use git branch -m (new name)

### Deleting

We can delete branches using **git branch -d (branch name)**, we cant delete the branch we are currently in, we must switch to an old/new one to delete said branch

Branches must be merged before being deleted, but if we are sure we want to delete said branch, we can use **-D**:

![image](https://github.com/user-attachments/assets/7574b7e5-3d00-4516-a622-be16de2020e1)

# Merging Branches 

## We can merge branches using **git merge (branch name)**

![image](https://github.com/user-attachments/assets/38013491-94c0-4cd4-a6cd-5a04b0e88d13)

The whole point of branching is to merge them in the end, but sometimes we would need to compare different branches and commit histories using **git diff**

## Git diff new commands 

Git diff commands with description:

![image](https://github.com/user-attachments/assets/bfdf3e22-1911-434e-8479-1091a761e458)

### git diff

Assume colors.txt is:

![image](https://github.com/user-attachments/assets/1ca462ec-b449-4a9e-af24-c3e3fcbdfdf3)

After changing Black to **Red** and running **git diff**

![image](https://github.com/user-attachments/assets/7c5bffc9-bb73-4e65-8206-a52bec3a4f64)

Changes compared between the staged file version of colors.txt and the non staged one.

### git diff --cached

To compare commit with staged, we commit colors.txt and then modify colors.txt to include new colors

![image](https://github.com/user-attachments/assets/258f78b9-9ec4-4ad4-b0a9-162848cb638f)

New colors.txt

![image](https://github.com/user-attachments/assets/022a7afc-8894-457a-83a6-5775009ec828)

Running the command

![image](https://github.com/user-attachments/assets/64c2514b-7e42-4adf-960a-8b7b50407b94)

### git diff HEAD

Compares the **unstaged changes** with the last commit histroy

Assume now that this is the last comitted version of colors.txt

![image](https://github.com/user-attachments/assets/cc59eeda-36db-4f2a-9c39-a56c138865cb)

We replace brown with magenta 

![image](https://github.com/user-attachments/assets/644b042d-3dd5-4c4b-8e3b-e6d6ec2ee27c)

### git diff -w 

Simply ignores whitespaces

### git diff commit 

Compares the **unstaged changes** (working directory) to a specific commit, basically like git commit HEAD just not the most recent commit

![image](https://github.com/user-attachments/assets/aef774de-59e3-4e4c-909e-6cec3f182488)

### git diff --cached commit

Compares the **staged changes** with a specific commit

![image](https://github.com/user-attachments/assets/39d242e8-4221-43a9-9f03-68b55cb03785)

### git diff commit1 commit2

Difference between 2 commits

![image](https://github.com/user-attachments/assets/13899545-832c-403a-a9a6-c3594cc0f0c5)

Note that its the same result as before, just with the markers swapped

## Comparing branches

We can compare branches using **git diff branch1 branch2**

![image](https://github.com/user-attachments/assets/47632400-30f4-4ea7-8d79-4f930586f6ea)

We can also see all changes in main since we branched from it

![image](https://github.com/user-attachments/assets/21373832-29ce-4615-ab9d-7155ae278cbd)

### git diff branch1 branch2 file.txt

Basically checks difference on a specific file

## Handling conflicts

![image](https://github.com/user-attachments/assets/3f28aa48-2daf-413f-bfaa-fed25b15fc31)

Here master has Coal and black, while newBranch has Gem

![image](https://github.com/user-attachments/assets/0792a805-8b79-4e28-ba0d-dce5da3d8f23)

When running git status, we can see the merge conflict 

![image](https://github.com/user-attachments/assets/5565e9e0-59e9-49af-8769-7f2698a4f870)

If the conflict is

- Hard to fix, Requires others help
- Can introduce a new bug

And other reasons, it would be best to aboirt using **git merge --abort**

Otherwise, like in our example, we can remove coal or black from the list of colors, **and remove conflict annotations**

![image](https://github.com/user-attachments/assets/cbd01c61-16a3-4e68-9c35-0e1ad6b08908)

Notice the updated MERGING near branch name

![image](https://github.com/user-attachments/assets/e3639446-4044-49b6-8819-44deefb98600)

After conflict is resolved, we commit and the merging happens, note that the MERGING status is no longer there.

# Remotes

Remote is basically a location where repo is hosted, like Github remote repositories

![image](https://github.com/user-attachments/assets/8116764e-5636-4767-bc14-6e55ff452573)

Common Remote commands

![image](https://github.com/user-attachments/assets/5439658a-a03c-4b6e-96e7-ff504687d10f)

git remove -v shows the remote repo ur working on

![image](https://github.com/user-attachments/assets/0b99c435-5aca-42a3-a0f2-640894af4d55)

We can create new files and push them into the repo using **git push**

![image](https://github.com/user-attachments/assets/499198b7-37a1-4c19-959b-a28098665d33)

![image](https://github.com/user-attachments/assets/99a50f4f-78ed-41ee-a21f-28fd0800ae0e)

If we add a file through github user interface, like this:

![image](https://github.com/user-attachments/assets/d21152f1-c880-4c19-8541-e12a945ce18e)

We need to update the remote in the command line

![image](https://github.com/user-attachments/assets/a4f58954-cea8-402d-baae-b4277e65c99b)

Notice the difference by 1 commit before and after **git remote update**, We can pull the changes using **git pull**, which does fetch (get any new files) + merge on any exisiting files we have.

![image](https://github.com/user-attachments/assets/3f1a0a2a-1dca-4dec-854d-17a3eea80580)

Now we are up to date with the origin/main

Assumw we do not do **git pull** when a feature4 is added

![image](https://github.com/user-attachments/assets/7595dba2-b8a3-4fd9-9d34-d965ed7cd259)

If we try to push changes we made, we get this:

![image](https://github.com/user-attachments/assets/926cdb62-b7ae-4cda-b947-76427a7e52bc)

To resolve the confict, we do git pull then push our changes.

![image](https://github.com/user-attachments/assets/23130a1e-96ef-4e53-ba64-d662ef8eca1a)

## Branches with remotes

![image](https://github.com/user-attachments/assets/b3c0a630-095a-43f9-9a4e-e31c2b5ff527)

We can also create branches and push/pull them into/from the remote repo using **git push -u origin (branch name)**

![image](https://github.com/user-attachments/assets/10b0a792-5dff-41b6-a0a3-c38e468a5cca)

And it will appear in the remote repo

![image](https://github.com/user-attachments/assets/d0a313be-e599-42b3-9a15-2253ebe413ce)

We can also run **git ls-remote** to see remote brnaches available

![image](https://github.com/user-attachments/assets/c5d090d1-b826-429e-a45b-86a421a207b2)

### Pulling a branch

To pull a branch from remote repo, we can use **git fetch origin (branch name)**, then **track** the branch in your local repo using **git checkout --track origin/(branch name)**.

Assume we created a new branch called thirdBranch on Github, or we pushed an existing one from our local repo

![image](https://github.com/user-attachments/assets/4f9f98d6-8a63-475a-93dc-db25ae3ad2cc)

![image](https://github.com/user-attachments/assets/4c8e43ae-ca88-4836-80df-06d1fbd81e44)

Note that we cant access or use the remote branch without **tracking** it

# Pull requests

![image](https://github.com/user-attachments/assets/9b9a0138-1907-4b6f-9b98-c7c2d7ea47a7)

![image](https://github.com/user-attachments/assets/bc39e5a7-a4ae-4ccf-a60a-c85862111fb8)

We created a new branch, called fourth branch, and made changes to the config.txt file in it and pushed the results into a new branch

![image](https://github.com/user-attachments/assets/04b82a1e-5302-4d22-bcf0-68e8b787b291)

Back in github, we now get this again

![image](https://github.com/user-attachments/assets/fa167e2c-741b-4d61-8df3-b017948cbe29)

Now we check the pull requests and the ability to merge, we can add reviewers to review our changes and add comments on them, and they can decide if:

1. Accept the changes
2. Request changes and wait for approval
3. Leave a comment, doesnt indicate approval

![image](https://github.com/user-attachments/assets/7ba3c5a8-8105-42e4-aa13-b85c4b8bb2b1)

![image](https://github.com/user-attachments/assets/9b970f74-184f-4a77-ab1f-c05714f719f4)

When scrolling down, we can see a short version of **git diff** command that compares main branch with the branch having a pull request:

![image](https://github.com/user-attachments/assets/7d31f9d8-c329-435c-8e75-cb47be268ff2)

After the pull request is created, we can merge it here and then delete the branch safely. 
![image](https://github.com/user-attachments/assets/5a5a09a2-a9fb-42a7-bee9-f6a4866b5c8c)
![image](https://github.com/user-attachments/assets/7d8016cb-6c96-4e19-987f-ec892817bf5e)

# GitIgnore

GitIgnore allows us to completely ignore files from the version control system, files added in the gitignore file are completely ignored by git.

![image](https://github.com/user-attachments/assets/04ac97da-89a4-4e93-9289-f10d4e27d952)

Examples

## .log files

When creating a file with .log extension, its ignored by git, notice here how test.log wasnt included in the **untracked files** in **git status**
![image](https://github.com/user-attachments/assets/cb345aca-a741-41d2-87fc-13f7f8d0b4e6)

## text file

To ignore a txt file for example, we can navigate to the **exclude** file and add it there.

![image](https://github.com/user-attachments/assets/c14d54de-f0e2-453c-8753-460a10e830b7)

![image](https://github.com/user-attachments/assets/5a487c74-1dbb-4baa-85ef-b25ed075f4e8)

We can also ignore all txt files by writing *.txt.

# Advanced Merging

## Git Rebase

![image](https://github.com/user-attachments/assets/4f5c233a-b4af-4fbc-81ad-18865c9d3ecd)

![image](https://github.com/user-attachments/assets/ad7eded2-83f4-41d1-9df0-7c4fa1fd59c8)

![image](https://github.com/user-attachments/assets/8ab438e4-637b-4c21-b8f3-06b643c188ba)

Rebase is basically squashing multiple commits we had into one commit, can be used to clean commit history and squash everything into one commit.

![image](https://github.com/user-attachments/assets/c2710795-6b8b-4f4b-9c0b-9f398c9b5962)

Here we have 3 commits, we can squash the 2nd and 3rd commit into the 1st commit, which would make it look like this

![image](https://github.com/user-attachments/assets/4dbbc229-47a1-4609-8bf5-25392a590f71)

We can then commit and it will appear as one commit in our history.

![image](https://github.com/user-attachments/assets/60a0d194-09dd-4119-ac1c-d8675e0202aa)

**Example**

We create a new branch and add a new file, and then make multiple commits on the same file

![image](https://github.com/user-attachments/assets/294c4ddb-04d6-4564-9f48-5705ca9f63bb)

From log, we can see the multiple commits.

![image](https://github.com/user-attachments/assets/bc285006-e0fa-4620-8285-997b077e1564)

To rebase we do this.

![image](https://github.com/user-attachments/assets/56653d2a-7070-4f75-ad5f-319887a3c810)

Notice how the first few characters from the "sha" are the same ones from the last main commit.

Now we do **git rebase -i commit sha**, which opens 2 pages

**First**

![image](https://github.com/user-attachments/assets/ff8af6a9-6a29-4a4a-a55b-3d8656327dec)

Originally, they are all **pick**, we change the 2nd and 3rd commits to **squash**, but leave the 1st one as it is, so we can squash into that commit, note that first one is typically set to pick as it serves as a base commit for all commits we want to squash, putting it as squash would do this.

![image](https://github.com/user-attachments/assets/f5769af1-c2e4-4515-81ba-8acaa82fed78)

Then after saving (using Esc + ":wq" on vin, depends on editor) 2nd page opens.

**Second**

![image](https://github.com/user-attachments/assets/9c47e7b3-0f8e-403b-bc5e-70a4cf2a5772)

Basically shows our commits with the commit message, we remove the first 2 and edit the last to include everything.

![image](https://github.com/user-attachments/assets/a0e7ce05-fe8c-4106-98bb-f0cd5ff022f6)

After saving again, we run git log and we can see the new squashed commit.

![image](https://github.com/user-attachments/assets/644057b9-805c-4956-a6f0-51e724e457ae)

## Rebasing from main

![image](https://github.com/user-attachments/assets/73338593-4e09-4afb-9201-c1848d92707b)

When we rebase from main, the new commit will be located before our branch commits, it basically creates a new copy of the **solution** branch commits, removes the original one, adds the rebase from main then adds the copies of the solution commits, the original branch commits will be handled using git grabage collection.

**Example**

Assume we have these commit logs

![image](https://github.com/user-attachments/assets/24a74646-d4bc-4fa7-8f16-42ddeb292c45)

Now we add a new file in main branch and commit.

![image](https://github.com/user-attachments/assets/0f5c29f1-bced-47fa-813e-def1959e0e98)

And we rebase from main in the second branch.

![image](https://github.com/user-attachments/assets/7fb8a00e-b717-4a37-8618-a236abc66f58)

Now we can see **main2.txt** in the second branch.

After running **git log --oneline**, we can see that Add main2.txt commit is before the commits of the second branch, even though it happened after.

![image](https://github.com/user-attachments/assets/06f04f85-2f82-463a-8395-2273ee7d9399)

Do note that the sha of the secondBranch commits are different from the original ones (before rebase).

## Cherry Picking

![image](https://github.com/user-attachments/assets/51e206d8-8705-4ce7-bdb2-18a5fecdd73a)

Basically means we can pick a commit from another branch that we can use in our branch, cherry picking should not replace merge, and it can also cause confusion. Like rebase, its an advanced git command that is not used often.

Here, we basically only need the last commit of X and Y for our feature, so we can **cherry pick** them into the feature branch and use them.

![image](https://github.com/user-attachments/assets/b4e7461e-0cfc-460f-9c39-1f6804a60c48)

**Commands**

![image](https://github.com/user-attachments/assets/f91aeee8-3f74-4087-9555-f484a4befc1d)


**Applying above diagram**.

We first add and commit a final feature file for this repo in main branch

![image](https://github.com/user-attachments/assets/022fae58-da5a-4637-a22e-16f9c0e8046a)

Then we branch to find X and Y

![image](https://github.com/user-attachments/assets/6a9b3642-5e78-4793-aff1-12ff27e2298a)

Now that we found the solutions, we can cherry pick them from main branch using the commit sha, and then we can see that the solution files are in the main branch

![image](https://github.com/user-attachments/assets/c8bb3c4b-5300-4ec8-ab59-a40ad0ebdbd8)

![image](https://github.com/user-attachments/assets/76f40b44-0d63-4565-a57d-22dcf2cf9ad6)

![image](https://github.com/user-attachments/assets/94ed8bae-ec91-4281-86b4-d49d3e06529a)

After the picking is done, we can see the old commit messages but with new "sha" in git log --online in main

![image](https://github.com/user-attachments/assets/9a2de812-a280-4bbf-9581-e1d731e1d952)
