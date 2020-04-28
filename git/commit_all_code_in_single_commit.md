# Commit all code in single sommit

Undo all the commits, merges, rebases etc. but PRESERVE the code and then we can commit the code in one single commit
```git
git reset $(git merge-base master $(git rev-parse --abbrev-ref HEAD))
```
