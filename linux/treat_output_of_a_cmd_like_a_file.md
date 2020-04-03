# Treat output of a command like a file

The output of a command can be treated like a file via `<(some command)` (known as process substitution). For example, compare local `/etc/hosts` with a remote one
```bash
diff /etc/hosts <(ssh somehost cat /etc/hosts)
```
