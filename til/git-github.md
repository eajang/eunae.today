---
description: All I have learned when I used git.
---

# Git / Github

## Add a Git Remote

```bash
git init
git remote add [remote-name] [remote-url]
```

To see the remote information:

```bash
git remote -v
```

To push all of your code to the new repository:

```bash
git fetch [remote-name]
git checkout master
git branch -u origin/master
git pull
git add --all
git commit
git push
```

## Add a Submodule

At the parent repository: 

```bash
git submodule add [remote-url]
```

After adding a submodule, you should commit the parent repository.

