# Don't clone entire repo history

To speed up git clone make sure you set the `--depth` option to 1 so you don't get the entire repository history. This is *very* useful when cloning repos in your CI.
```bash
git clone [REPO] --depth 1

# When you don't need the entire history of a repo, you can speed up git clone by specifying the number of revisions you need
```
