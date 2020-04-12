# Docker Cheat Sheet
Most commonly used docker commands

### CONTAINERS
- Start a running container from an image
 `docker run -ti ubuntu bash`
    

- List running containers
 `docker ps`

- List stopped containers
`docker ps -a`

- List last container 
`docker -l`

- Delete a container after it finishes
`docker run -ti --rm ubuntu bash`

- Commit a container and create a new image from it. First find the container id or its name then run the following command. Lets say 1234 is container id and my_container is the name
`docker commit 1234 new_image_name`
OR
`docker commit my_container new_image_name`

- Attach an existing running container
`docker attach name_of_container`
- Now leaving container wihtout exiting it
`press and hold ctrl + p, ctrl + q`

- docker exec creates a new process in the existing container. Although it will die automatically if you close the original process

- docker logs will print the logs of the container
`docker logs container_name`

- docker kill will kill the running container
`docker kill container_name`

- Removing containers
`docker rm container_name`

- If the outside ports are not assigned then it will choose any available port. To see which port it choose, run the following command
`docker port container_name`

### NETWORKS
- For displaying list of already existing networks.
`docker network ls`

- For creating a new network
`docker network create new_network_name`

- for starting a container within a network
`docker run -ti --net my_network_name --name my_container_name ubuntu bash`


### VOLUMES
 - 2 main varieties of volumes
	**Persistent** --> they will still exist when the contaner is stoppe 
 	**Ephemeral** --> they will be gone when no one (container) is using them

- Sharing a volume with the host (Persistant)
`docker run -ti -v /full/path/to/folder:/shared_folder ubuntu bash`

- Sharing a volume b/w containers using volume-from (Ephemeral)
`docker run -ti -v /shared-data ubuntu bash`
	 - In above command Im creating a shared volume on the container that is not shared with the host
	 - Now create another container and shared the above volume with the new continer
`docker run -ti --volume-from above_container_name ubuntu bash`
	 - Now important note: The above volume will be available as long as atleast one container is still using it. when no container is active that volume will disappear
