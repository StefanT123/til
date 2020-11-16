# Make backup of untracked files

Most of the time, it’s safe to delete all the untracked files. But many times, there is a situation wherein you want to delete, but also to create a backup of your untracked files just in case you need them later.
```bash
git ls-files --others --exclude-standard -z | xargs -0 tar rvf ~/backup-untracked.zip
```
