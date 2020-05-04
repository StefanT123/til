# Compare local and remote files

```bash
ssh user@remote-host "cat /home/root/file_remote" | diff  - file_local
```
