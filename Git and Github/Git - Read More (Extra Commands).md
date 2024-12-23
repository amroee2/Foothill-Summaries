# Git Reflog

Reference logs, or "reflogs", record when the tips of branches and other references were updated in the local repository. Reflogs are useful in various Git commands, to specify the old value of a reference.

**HEAD@{1}** Basically means what state head was in one change ago.
![image](https://github.com/user-attachments/assets/c863640a-930a-4dc1-8201-2344e0414348)

It can take a couple subcommands 

When running **git reflog**, **show** is the default subcommand.

![image](https://github.com/user-attachments/assets/98f9d090-e91f-4072-b357-77d87ecbbc86)

## Delete

**git reflog delete** deletes a certain reflog

![image](https://github.com/user-attachments/assets/0fdeea6d-e2f5-469a-9715-df652cd1f10b)

From git reflog the previous **HEAD@{1}** is not there anymore, and the number of logs went down to 29.

**before**

![image](https://github.com/user-attachments/assets/d6779e2e-31d6-4629-8e2c-029e80113396)

**after**

![image](https://github.com/user-attachments/assets/fa8e2b55-3638-4acf-90d7-917b1b088f7d)

But we can still see the commit itself in git log.

![image](https://github.com/user-attachments/assets/952f83d2-dfde-4cbe-b102-f76e8a1018d4)

# Git bisect

Runs a binary search algorithm to find a commit the user is looking for, can be used to find a commit that introduced a bug/feature, or if you want to find a commit where a new specific change happened. Git bisect can be ran like this.

We can start a bisect "session" through **git bisect start**, then it would expect 2 commands, **git bisect bad (commit sha)** (if no sha specified it will take the most recent commit as the bad one) to set the bad commit and **git bisect good (commit sha)** to set the good commit, then it posts every commit in between with the commit message and then we can decide if this commit is a bad or a good one, then it posts the ones we labeled as bad at the end.

![image](https://github.com/user-attachments/assets/5bb7a1af-9272-439c-856f-30514ad4927b)

then run **git bisect reset** to exit.

you can replace **bad** with **old** and **good** with **new** to find a commit that didnt introduce a bug but a feature or if you want to find a commit for other reasons, **you cant use one of each with the other**.

# Git hooks

Git hooks are scripts that Git executes before or after events such as: commit, push, and receive.

Hooks are located in the .git/hooks directory.

![image](https://github.com/user-attachments/assets/5839b208-64d6-483a-a8d1-cd206ee9954f)

![image](https://github.com/user-attachments/assets/d8a7db37-6800-4702-8146-a5103dddbc23)

To activate a hook from the predefined ones from git, we can rename the file and remove the .sample part. pre-commit pre-defined hook checks for trailing white spaces.

![image](https://github.com/user-attachments/assets/7096e4a0-571c-4f03-96af-904f1f8846c8)

![image](https://github.com/user-attachments/assets/44c8ad9f-0370-4cc6-852e-bf04adbfaeb2)

![image](https://github.com/user-attachments/assets/2b8a9808-9f54-444d-a120-1af2b7d65806)

**Simple custom hook**

First, we can put the .sample back on the pre-commit file and then create our own pre-commit hook, then make all hooks executable using **git config core.hooksPath .git/hooks**, and finally write our own custom hook in python or any other programming languages.

![image](https://github.com/user-attachments/assets/5ff1c222-98d5-4ec7-9435-9d0e9595bcf5)

There are 2 types of hooks

- Client side hooks: Such as **pre-commit** hook, they basically are related to the local repository such as committing, rebasing, merging and pushing.

- Server side hooks: They relate more to remote repository, like **pre-recieve**, **update** and **post recieve**.

# Git blame

Git blame takes a file as an argument and shows lines with their author, date and the commit SHA, **we make sure to pass -w to ignore whitelines**

![image](https://github.com/user-attachments/assets/41509738-014d-4bb5-b96e-89f092cad513)

It's also possible to view the blame command output through github UI

![image](https://github.com/user-attachments/assets/e98b428c-6701-4f8a-b7ed-6acc7b84b050)

Its useful when trying to find out why a certain line/chunk of code was introduced, as we can find the commit and find its details using git cat-file or git show. 

# Git submodule

git submodule is a way to have a repository as a directory of an another repository.

**git submodule add (repository url)**

![image](https://github.com/user-attachments/assets/07b9623f-0ea8-4181-a22a-e8be49d63672)

We can see that a file and a directory were created, .gitmodule file contains the configurations for all submodules, it includes the path and the url for each, while the directory is the new repository.

![image](https://github.com/user-attachments/assets/36ae0ee8-53fb-4b0c-88f7-4603cd50ac3a)

![image](https://github.com/user-attachments/assets/0001d445-4f2f-4681-a0d8-e50d1a8ec776)

![image](https://github.com/user-attachments/assets/8b4ce312-ad8e-4682-a650-a23901794c06)

When making a commit within the submodule, the outer module will track these changes as well.

![image](https://github.com/user-attachments/assets/df627fa9-97f7-4be6-9d99-c8c102432b2c)

In github, a submodule repository looks like this.

![image](https://github.com/user-attachments/assets/dd36ca91-aa7b-47df-b765-71cc0bd78a16)

If you push the chnges only in the outer repository and not in the submodule, we will be redirected to a 404 page.

![image](https://github.com/user-attachments/assets/04854024-2996-4933-9ab5-04e7d74ced8a)

![image](https://github.com/user-attachments/assets/4eca32e5-32d2-4b13-96e9-c697ec580527)

But after we push the changes, the page will open, as its basically just a reference to the last commit the submodule had.

![image](https://github.com/user-attachments/assets/06ea6611-6c18-4df0-9e85-0cd311748f6e)
