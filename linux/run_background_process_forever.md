# Run background process forever

Run process that can live beyond the terminal:
`nohup command options`

---

Allow sub-processes to live beyond the shell that they are attached to.

Disown the current job:
`disown`

Disown a specific job:
`disown %job_number`

Disown all jobs:
`disown -a`

Keep job (do not disown it), but mark it so that no future SIGHUP is received on shell exit:
`disown -h %job_number`

---

Display status of jobs in the current session.

Show status of all jobs:
`jobs`

Show status of a particular job:
`jobs job_id`

Show status and process IDs of all jobs:
`jobs -l`

Show process IDs of all jobs:
`jobs -p`
