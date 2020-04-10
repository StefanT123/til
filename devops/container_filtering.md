# Container filtering

Get a list of all non-running (stopped) containers
`docker container ls -a --filter status=exited --filter status=created`

Remove all containers that are created more than 12 hours ago
`docker container prune --filter "until=12h"`
