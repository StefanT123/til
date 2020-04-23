# Push to multiple git repos

If a project has to have multiple git repos (e.g. Bitbucket and Github) then it's better that they remain in sync.

Usually this would involve pushing each branch to each repo in turn, but actually Git allows pushing to multiple repos in one go.

We can setup push URLs like this
```git
git remote set-url --add --push origin git@github.com:muccg/my-project.git
git remote set-url --add --push origin git@bitbucket.org:ccgmurdoch/my-project.git
```

It will change the `remote.origin.pushurl` config entry. Now pushes will send to both of these destinations, rather than the fetch URL.

### Per-branch

A branch can push and pull from separate remotes. This might be useful in rare circumstances such as maintaining a fork with customizations to the upstream repo. If your branch follows `github` by default:
```git
git branch --set-upstream-to=github next_release
```
(That command changed `branch.next_release.remote`)

Then git allows branches to have multiple `branch.<name>.pushRemote` entries. You must edit the `.git/config` file to set them.
