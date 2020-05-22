# Embed a comments within a chain of commands

```bash
echo before && : this  && echo after

(echo banana; : THIS IS SOME COMMENT) | tr 'b' 'm'
```
