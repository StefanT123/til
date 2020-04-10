# Remove images

`docker image rm {image-id} {image-id2}`

Remove dangling images
`docker image prune`

Remove all unused images
`docker image prune -a`

Remove all images created more than 12 hours ago
`docker image prune -a --filter "until=12h"`
