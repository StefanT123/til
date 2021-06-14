# Search for some string in commits

```git
git grep {string} $(git rev-list --all -- {some/file}) -- {some/file}
```
