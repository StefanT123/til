# Remove everything (all dangling images, stopped containers, all unused netwroks)

`docker system prune`

If you also want to remove all unused volumes, pass the `--volumes` flag
`docker system prune --volumes`
