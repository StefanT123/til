# Delete references of remote branches that don't exist

This will prune all those non-existent remote tracking references which is sure to clean up your git log
```git
git fetch origin --prune
```
