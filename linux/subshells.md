# Subshells

In Bash scripts, subshells (written with parentheses) are convenient ways to group commands. A common example is to temporarily move to a different working directory
```bash
# do something in current dir
(cd /some/other/dir && other-command)
# continue in original dir
```
