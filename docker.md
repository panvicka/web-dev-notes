## Learn Docker - DevOps with Node.js & Express
... from *freeCodeCamp.org* 


- create Dockerfile, copy package.json first, then `npm install` and then copy the rest of the app 
- `docker build .`
    - `-t name-of-image` 
- docker has cache, it only runs steps if something changes 
- `docker image ls` to see images 
- `docker image rm ID`
- `docker run CONTAINER-IMAGE-NAME`
    - `--name CONTAINER-NAME`
    - `-d` to run in detatched mode