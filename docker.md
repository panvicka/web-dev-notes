## Learn Docker - DevOps with Node.js & Express
... from *freeCodeCamp.org* 

- first if the docker is not running due ti problems with permission run `sudo chmod 666 /var/run/docker.sock` 


- create Dockerfile, copy package.json first, then `npm install` and then copy the rest of the app 
- `docker build .`
    - `-t name-of-image` 
- docker has cache, it only runs steps if something changes 
- `docker image ls` to see images 
- `docker image rm ID`
- `docker run CONTAINER-IMAGE-NAME`
    - `--name CONTAINER-NAME`
    - `-p` 3000:4000 -> 4000 is the container expecting port, 3000 is the port on host machine that should be connected to container 
    - `-d` to run in detached mode
- `docker rm CONTAINER-NAME -f` with `-f` flag you can delete running container 
- `docker exec -it CONTAINER-NAME bash` to have a look inside container (-it for interactive)
    - exit with `exit` 
- volumes allows us to have persistent data, special type of volumes are "bind" volumes. They sync folder or file system with files in container. This is good for developing, the code updates itself without having to build and start container over and over again 
    - `docker run -v pathToFolderOnLocal:pathToFolderOnContainer:/app`, app or any other folder inside container
    - current folder on windows cmd `%cd%`, windows powershell `${pwd}`, linux `$(pwd)`
    - if you are developing with express, node or something like that, you need to restart the process when the code changes, use `nodemon` or something :) 
- `docker ps -a` show all containers, even the stopped ones
- `docker longs CONTAINER-NAME` shows log from container 
- if case the container doesn't work when node_modules are removed locally with active volume bind
    - the syncing bind volume will also remove node_modules in the container :( 
    - solution: create anonymous volume. Volume works based on specificity, we can create a subfolder as volume and this wont be overwritten as it is more specific 
    - `-v /app/node_modules`- this is like "do not touch node_volumes folder
    - also syncing works both way, so the changes made by container can change files on our local machine 
        - potential security issue, we can make the bind read only `$(pwd):/app:ro`, ro - read only 
- environmental variables
    - check environmental variable, go to `docker exec CONTAINER-NAME -it bash` and `printenv`
    - pass env variable directly `docker run --env PORT=4000`
    - or with file `docker run --env-file ./.env`
- show volumes created by docker `docker volume ls`, they build up. Deleting container wont delete the anonymous volume.
    - `docker volume prune` removes volumes that are no longer needed 
    - or when you delete docker with `rm` add `-v` so `docker rm CONTAINER-NAME -fv`
- docker compose to automate build&run steps in `docker-compose.yaml` file...
    - each container is a service  
    - bring up with `docker-compose up`, it doesn't rebuild it again until said because it only looks for image, force it with `-build`
    - or down with `docker-compose down` or with deleted volumes `-v`