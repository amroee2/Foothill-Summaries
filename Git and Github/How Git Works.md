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

![image](https://github.com/user-attachments/assets/029825b2-7438-4ad8-bccb-e7d307bb6215)

When we do the opposite, as in be in the ideas branch and merge with master, a new commit will not occur, it will just change the branch reference commit to the new merge commit.

![image](https://github.com/user-attachments/assets/4ff2a6c8-eb48-4196-800e-bde889cacc0e)

This is called a **fast forward merge**.
