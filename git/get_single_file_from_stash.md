# Get a single file from stash

In git, you can reference a commit SHA or branch to checkout differing versions of files.
```git
git checkout d3d2e38 -- README.md
```

In the same way, you can snag the version of a file as it existed in a stash. Just reference the relevant stash.
```git
git checkout stash@{1} -- README.md
```
