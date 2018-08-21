```
docker login

docker run <image>
# running in background and correct url will be http://localhost:4000
docker run -d -p 4000:80 <name>

# list docker images
docker image ls

# list running docker containers
docker container ls

# create docker image 
docker build -t <name>

docker container stop <containerID>

# stop and remove image
docker rm -f <name>

docker tag image username/repository:tag
```

Links   
https://docs.docker.com/get-started/part2/#tag-the-image   
https://github.com/docker/labs/blob/master/beginner/chapters/setup.md
