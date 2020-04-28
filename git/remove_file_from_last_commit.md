# Remove a file from last commit

We can use the `rm` command to remove the old file and then run `git commit --amend` to amend the last commit to remove the file.
```git
git rm —-cached file-to-remove
git commit —-amend
```
