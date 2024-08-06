# How Git Works

Git can be extremely confusing when working with it, and it might feel like there is a lot going on at the same time, so understanding how git works from the inside can help improve the understanding of git.

## 2 types of git commands

## Porcelain commands 

These are high level commands that users might have worked with all/most of them.

![image](https://github.com/user-attachments/assets/58a101c0-5d68-4478-9d47-23692c2f6219)

## Plumbing commands

These are the low-level commands, which are ones rarely used and concerns the inner details of git.

![image](https://github.com/user-attachments/assets/6fd399d2-610a-4920-ae5e-a5783c4e51aa)

## Git from the inside layers

Ignoring the whole distributed version control system, branches and such, git from the inside is just a map that maps keys and values using SHA1 (Secure Hash Algorithm 1).

Each **object** in git has a **unique** hash code, the probability of a collision happening in git equals probability of winning the jackpot 6 times in a row (Winning it once is one in a 170 million).

### Git hash-object

Returns the hash code of the object, like this.

![image](https://github.com/user-attachments/assets/01a502f0-f122-4a0b-827c-801ab6b6f973)

If we run the command again, it will output the same hash code. Git generally outputs the same hash code for the same content for everyone, even across different OS, but in Linux this command would output a different hash code simply because windows handles the **echo** command differently, it takes the string quotations into account and adds a null terminator at the end.

We can store the hash for an object like this.

![image](https://github.com/user-attachments/assets/d2faba6e-fac7-4d4d-a524-cff3eaba5eae)

In linux, Apple Pie hash code looks like this

![image](https://github.com/user-attachments/assets/0d78aa0e-bc4f-401d-9252-82cff44a4b63)

They share almost the same sha but with some different characters.

Then using explorer .git in windows, we navigate to Objects.

We can see a folder named "23", which are the first 2 characters of the Apple Pie hash code.

![image](https://github.com/user-attachments/assets/3c8b2e43-952f-4008-ab36-ebdea5683c2d)

And inside are the remaining characters

![image](https://github.com/user-attachments/assets/914467dc-fc17-4614-a6ac-cee7ffe1eeb1)

This is called a blob, its a generic piece of content and it represents the files in git.

We can check the type and content of a hash code using **git cat-file**

![image](https://github.com/user-attachments/assets/4a428383-a182-457c-9e1d-0934d13b79e9)

## Next layer in git

Now that we have seen how git stores things in a key value map, the next layer of git is the content tracker layer, which is the description of git when running **man git** in linux.

When running the same command on a commit sha (can be found using **git log**) we can see this.
![image](https://github.com/user-attachments/assets/af7d66f8-1df0-4ede-ad7a-88fc89b302fd)

It outputs the author and committer information, as well as the date in a number format in the end, it also outputs a **tree**, which is a new object type like **blob** in git, unlike blob, tree represents the **directory** in git.

When we access the tree using the same command, we would be able to see other objects inside it, in linux recipe.txt would have the same SHA1 code with "Apple Pie", but since windows handles file saving differently, sha1 is different.
![image](https://github.com/user-attachments/assets/a5d4d33f-16c2-4ced-879a-7ad617faa950)

If we make changes to recipe.txt and commit and then access the new commit SHA1, we can see the new parent line, which is the SHA for the previous commit.

Commits are also an object type in git.
![image](https://github.com/user-attachments/assets/d1d1889a-66cb-49d4-9a18-601956f6d826)

There are 4 object types in git

- Blobs
- Trees
- Commits
- Annoated tags (discussed later).

# How Branches Really Work

Branche are just references to commits, thats all.

In .git folder, we can navigate to refs/heads and see all our branches, currently there is only one branch

![image](https://github.com/user-attachments/assets/9096adeb-c90a-49b4-984f-2c2b5d0fc171)

Now after we create a new branch, its added into that same heads directory

![image](https://github.com/user-attachments/assets/cf0e50c7-d7e1-49b4-a994-2c0fa154f340)

Notice that the content of the files are just references to commits, and since we just created the ideas branch, it will reference the same commit as the master one

![image](https://github.com/user-attachments/assets/9752a583-c7c0-400e-b294-191b8d0a92cd)

**How does git know which branch we are in?**

Git knows using the HEAD file in .git dir

![image](https://github.com/user-attachments/assets/13fc6f81-1675-4b9a-99d1-edd7ca7d0f67)

![image](https://github.com/user-attachments/assets/69deccae-5ec5-4998-bfd9-8ba5976c0acb)

basically contains the path to the said file.

Now after making a new commit in master, we can see that the reference main to a commit changed, but **head didnt**, head simply went along with main, if we switch to the ideas branch, we will go back to the previous commit.

![image](https://github.com/user-attachments/assets/cd78fc61-1346-487f-9da5-8a26ba35c7ca)

Head only changes when we switch branches.

## Merging

We can update the recipe.txt file in the ideas branch and then merge in the main branch to see what happens.

![image](https://github.com/user-attachments/assets/f31bd77a-09a1-41fe-a052-e389c69e19cc)

Conflict occured, we can resolve the conflict by making some changes to the recipe and remove the annotations.

![image](https://github.com/user-attachments/assets/65a46623-8754-4e4d-b756-b9212a94d412)

after handling the conflict, we can see that the main branch refeerence was updated to the merge commit.

![image](https://github.com/user-attachments/assets/e2a6766e-8a79-4760-a534-07d3a5e9780d)

And using **git cat-file** we notice that this time the commit has 2 parents, which are basically the commits we merged, after the operation is done, main gets updated to reference the merge commit like we said, but ideas stays where it is.

![image](https://github.com/user-attachments/assets/86d78fda-36d6-41a7-a0bc-d920c268a236)

![image](https://github.com/user-attachments/assets/029825b2-7438-4ad8-bccb-e7d307bb6215)

When we do the opposite, as in be in the ideas branch and merge with master, a new commit will not occur, it will just change the branch reference commit to the new merge commit.

![image](https://github.com/user-attachments/assets/4ff2a6c8-eb48-4196-800e-bde889cacc0e)

This is called a **fast forward merge**.

# Losing your HEAD

In git, you can use HEAD to refer to a **commit**, this is done using **git checkout (commit sha)**.

![image](https://github.com/user-attachments/assets/3c8c1a4c-21f0-4da3-9c4c-63c2188fc6c7)

Notice the new status in place of branch name.

Notice that head now acts as a branch, it shows the most recent commit for it and the commits before it.
![image](https://github.com/user-attachments/assets/91f335e6-ff89-4fda-9b6c-50923c5f2c1c)

Notice how HEAD now contains the commit SHA

![image](https://github.com/user-attachments/assets/01e93a10-564c-42b6-9177-d1add86cfc07)

And since its an old commit, it also has the old version of recipe.txt 

![image](https://github.com/user-attachments/assets/5bd665f4-a2f8-4e28-9b5b-b80eb78cef93)

Since it works like a branch, we can make changes and commit as usual.

![image](https://github.com/user-attachments/assets/ad3e1c6d-8dc4-4848-8fbe-a9cbe3c2b983)

**What happens when you switch back to master?**

The new commits can be at risk of being garbage collected, to avoid this, we could add a branch using **git branch (branch name) last commit sha)**

Notice now that the new commit is not included in master branch log.

![image](https://github.com/user-attachments/assets/220b441c-fc1a-4ab4-85ef-3d3e24265920)

But now we can switch to headBranch and work as usual

![image](https://github.com/user-attachments/assets/aae3fe6b-2d30-4485-baf6-957b3dcef406)

Now we can merge into main, resolve conflict and log would look like this

![image](https://github.com/user-attachments/assets/43f0f36b-e38e-4ab5-934b-cb9489adb9f6)

Finally we can go to main and merge with head branch (fast forward) and do the same with ideas. It would look like this in the end.

![image](https://github.com/user-attachments/assets/a3ca9395-51b2-43e0-92dd-f9f1e4c11c60)

# Rebasing from the inside

Rebasing, like mentioned before is an advanced type of merge, when rebasing from main branch, we take all the second branch commits, make a copy of them and put them ahead of all main branches commits.

![image](https://github.com/user-attachments/assets/84a325e6-2df1-428b-bf41-51faac51dbcd)

Merges are simpler, as they just create a new commit that has 2 parents, **rebasing** can be a dangerous process since it **forges history**, like in the picture above, it might seem like these commits were in order, but in fact there is a chance that we commited in main branch after our last commit in the second branch, and after rebasing **all** main commits are now before the second branch commits.

**When in doubt, use merge**

# Introduction to Tags

Tags are the fourth object type in git.

![image](https://github.com/user-attachments/assets/6975f67a-9488-40c6-8c37-d9150586beb9)

They are used to put a label on a commit.

## Annotaed tag

An annotated tag is a label for a commit with a message.

![image](https://github.com/user-attachments/assets/2fe1ed88-f87f-40a7-8e23-94ddb5a74aa2)

Tags are stored in the same directory as baranches.

![image](https://github.com/user-attachments/assets/764405a8-2e94-4edf-b386-127bbf86d4f2)

When doing cat-file on a tag, it outputs a paragraph containing

- Hash code for an object (the commit it tags)
- Author name and email
- Date
- And the message

![image](https://github.com/user-attachments/assets/b9c7d84a-f63b-402f-9db3-3eb512839b5d)

We can see that the hash code is the same one shown when using **git log**.

![image](https://github.com/user-attachments/assets/67b98821-e29f-4e7c-a6a4-06044603f72a)

We can also checkout a tag as well, and do the detached HEAD process all over again.

Unlike branches, tags are associated with commits, when you add a new commit, the branch ref changes, but the tag stays the same.

## Lightweight tags

Works the same as annotated tags, but without storing all those additional information, it only contains the commit SHA its referring to.

We do **git tag (tag name)**, in this case we did **git tag newTag**

![image](https://github.com/user-attachments/assets/5743ef85-6161-4282-8761-319d086576fb)

Its stored in the same directory as annotated tags, and it only contains the commit SHA, Notice how they are the same.
![image](https://github.com/user-attachments/assets/a1e6e3e8-794c-4dee-94a5-3c832a33045c)

The main difference between annotated tags and Lightweight ones is that annotated tags have additional metadata that points to the commit, lightweight ones refer to the commit directly, and are clsoer to the concept of **branches** than annotated ones, but unlike branches, it doesnt update after committing.

![image](https://github.com/user-attachments/assets/dd896c96-3e52-462a-b271-b732a73cc8b5)

And this completes version control layer.

# Distributed Version Control

The whole point of git is to keep track of versions of our project but to also work with others on said projects, which is why we have systems like Github where git is hosted on it.

A Github repo is a **remote repo** that people working on the same project can clone and work on, and then pull/push changes depending on the workflow.

## git push

Git push is used to upload the files/changes we worked on into the remote repo, and depending on the current state of the repository our changed will show up on github.

When another user uploads their changes, they will have to **pull** the repo first, so they can **fetch** the changes we worked on and then **merge** their work with our work, handle any conflicts (if exist) then push the changes.

**git pull** is a mix of **git fetch** and **git merge**, we can either do git pull directly or do the other 2 seperately.

## Issue with Rebase

Assume we are in this situation, we rebased in our local repo and want to push changes into the remote repo, but this will cause conflicts because we have different histories on the local and remote repos.

![image](https://github.com/user-attachments/assets/be85b5ac-81cd-4833-8d5d-a360363a2bc1)

So to solve the confict we can either do **git push -f** which is not a good idea, or we can pull and handle the conflict locally.

Only this time the result is not great, now we have a 2 of the same commit, the original commit and the new copy of it that was created during rebase operation, this will cause confusion (2 commits with the same version of files, same commit message, just different SHA1) and is against the whole point of rebasing (cleaning commit history).

![image](https://github.com/user-attachments/assets/ab71a668-dd62-47be-854a-a2739e239aae)

To avoid this, as a rule of thumb we shouldnt rebase shared commits (a commit that has been pushed into a shared repoistory).
