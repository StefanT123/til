# Get container IP address

`docker inspect -f \"{{ .NetworkSettings.IPAddress }}\"`
