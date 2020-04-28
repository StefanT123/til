# Get containers IP inside a specific network

`docker inspect -f '{{.NetworkSettings.Networks.[network].IPAddress}}' [container]`
