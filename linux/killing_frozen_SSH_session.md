# Killing A Frozen SSH Session

Whenever an SSH session freezes, I usually mash the keyboard in desperation
and then kill the terminal session. This can be avoided though. SSH will
listen for the following kill command:

```
1. press enter
2. write ~ (tilde)
3. write . (period)
```

This will kill the frozen SSH session and leave you in the terminal where
you were before you SSH'd.
