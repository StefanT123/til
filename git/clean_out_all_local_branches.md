# Clean out all local branches

Sometimes a project can get to a point where there are so many local branches that deleting them one by one is too tedious. This one-liner can help:
```git
git branch --merged master | grep -v master | xargs git branch -d
```

This won't delete branches that are unmerged which saves you from doing something stupid, but can be annoying if you know what you are doing. If you are sure you want to wipe everything, just use `-D` like so:
```git
git branch --merged master | grep -v master | xargs git branch -D
```
