# Open all files with conflicts at once

```git
git diff --name-only --diff-filter=U | uniq  | xargs $EDITOR
```
`—-diff-filter=U` filters out all the files without conflicts.
