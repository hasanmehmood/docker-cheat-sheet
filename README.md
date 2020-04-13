## Docker Cheat Sheet

### CONTAINERS

- Start a running container from an image<br>
 `docker run -ti ubuntu bash`
 
- List running containers<br>
 `docker ps`

- List all containers (stopped & running)<br>
`docker ps -a`

- List last container <br>
`docker -l`

- Delete a container after it finishes<br>
`docker run -ti --rm ubuntu bash`

- Commit a container and create a new image from it. First find the container id or its name then run the following command. Lets say 1234 is container id and my_container is the name<br>
`docker commit 1234 new_image_name`
OR<br>
`docker commit my_container new_image_name`

- Attach an existing running container<br>
`docker attach name_of_container`
- Now leaving container wihtout exiting it<br>
`press and hold ctrl + p, ctrl + q`

- docker exec creates a new process in the existing container. Although it will die automatically if you close the original process

- docker logs will print the logs of the container<br>
`docker logs container_name`

- docker kill will kill the running container<br>
`docker kill container_name`

- Removing containers<br>
`docker rm container_name`

- If the outside ports are not assigned then it will choose any available port. To see which port it choose, run the following command<br>
`docker port container_name`

### NETWORKS
- For displaying list of already existing networks.<br>
`docker network ls`

- For creating a new network<br>
`docker network create new_network_name`

- for starting a container within a network<br>
`docker run -ti --net my_network_name --name my_container_name ubuntu bash`


### VOLUMES
 - 2 main varieties of volumes<br>
	**Persistent** --> they will still exist when the contaner is stopped <br>
 	**Ephemeral** --> they will be gone when no one (container) is using them<br>

- Sharing a volume with the host (Persistant)<br>
`docker run -ti -v /full/path/to/folder:/shared_folder ubuntu bash`

- Sharing a volume b/w containers using volume-from (Ephemeral)<br>
`docker run -ti -v /shared-data ubuntu bash`
	 - In above command Im creating a shared volume on the container that is not shared with the host<br>
	 - Now create another container and shared the above volume with the new continer<br>
`docker run -ti --volume-from above_container_name ubuntu bash`
	 - Now important note: The above volume will be available as long as atleast one container is still using it. when no container is active that volume will disappear<br>
