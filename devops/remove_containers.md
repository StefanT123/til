# Remove contianers

`docker container rm {container-id} {container-id2}`

Remove all stopped containers
`docker container prune`

Stop and remove all containers
`docker container stop $(docker container ls -aq)` - stop the containers
`docker container rm $(docker container ls -aq)` - remove the containers
