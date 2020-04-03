# Find and kill processes by name

Return PIDs of any running processes with a matching command string
`pgrep {some_process}`

Search full command line with parameters instead of just the process name
`pgrep -f "process_name parameter"`

Search for process run by a specific user
`pgrep -u root process_name`

---

Kill all processes which match:
`pkill -9 process_name`

Kill all processes which match their full command instead of just the process name:
`pkill -9 -f "command_name"`

Send SIGUSR1 signal to processes which match:
`pkill -USR1 process_name`

