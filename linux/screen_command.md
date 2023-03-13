# Screen command

screen command in Linux provides the ability to launch and use multiple shell sessions from a single ssh session. We can use this command to detach when we are running some time-consuming operation and reatach later.

```bash
# When we ssh into some server we can create separate session
screen -S session_name

# then we can run some time-consuming command into that session

# after we had started some command we can detach from that session and let the command run
screen -d screen_id
# or with CTRL + a, CTRL + d in the screen session

# to see all started sessions
screen -ls

# to join some detached session
screen -r session_name

# to kill the session, just type exit and hit enter in the session you want to kill
```
