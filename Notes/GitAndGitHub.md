
```
git -v
git version 2.42.0

>> git status
>> git init

>> git add .
>> git commit -m "message"
>> git commit -am"message"

>> git log


>> git branch
>> git branch feature
>> git switch feature
>> git switch -
>> git checkout feature

>> git switch -c test (new branch as test will be created and switched to test branch)

>> git checkout -b anotherTest (new branch as anotherTest will be created and switched to anotherTest branch)

>> git branch -d anotherTest (to delete branch)
```

```
# Linux
- ls
- ls -a (show hidden files)
- ls -al
```

To switch to the `origin/category-dto-mapper` branch, you need to create a local branch that tracks the remote branch. Here's how you can do it:

### Step 1: Fetch the latest remote branches
Ensure you have the latest information about remote branches by running:

```bash
git fetch
```

### Step 2: Create and switch to a local branch that tracks `origin/category-dto-mapper`
Run the following command:

```bash
git checkout -b category-dto-mapper origin/category-dto-mapper
```

### Explanation:
- `git checkout -b category-dto-mapper`: Creates a new local branch named `category-dto-mapper`.
- `origin/category-dto-mapper`: Specifies the remote branch that the new local branch should track.

### Step 3: Verify the switch
After running the above command, you can verify that you are now on the `category-dto-mapper` branch by running:

```bash
git branch
```

You should see an asterisk (`*`) next to `category-dto-mapper`, indicating that it is the current branch.

### Step 4: Check the status
You can also check the status of your working directory to confirm everything is up to date:

```bash
git status
```

This should show that you are on the `category-dto-mapper` branch and that your working tree is clean (or show any changes if there are any).

### Example Workflow:
```bash
swapnilk~$ git fetch
swapnilk~$ git checkout -b category-dto-mapper origin/category-dto-mapper
Branch 'category-dto-mapper' set up to track remote branch 'category-dto-mapper' from 'origin'.
Switched to a new branch 'category-dto-mapper'
swapnilk~$ git branch
* category-dto-mapper
  dev
  master
swapnilk~$ git status
On branch category-dto-mapper
Your branch is up to date with 'origin/category-dto-mapper'.

nothing to commit, working tree clean
```

Now you are successfully switched to the `category-dto-mapper` branch!
