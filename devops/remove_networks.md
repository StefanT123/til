# Remove networks

`docker network rm {network-id}`

Remove all unused networks
`docker network prune`

Remove using filters
`docker network prune -a --filter "until=12h"`
