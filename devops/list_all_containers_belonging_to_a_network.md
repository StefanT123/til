# List all containers belonging to a network

`docker network inspect -f '{{range .Containers}}{{.Name}} {{end}}' [network]`
