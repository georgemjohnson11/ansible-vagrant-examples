https://docs.docker.com/get-started/



I run my own local docker registry by running this in my terminal: 
> docker run -d -p 5000:5000 --restart=always --name registry registry:2

From this directory, run this in the terminal to build the dockr image: 
> docker build -t friendlyhello .

After building an image, the container can be ran in detached mode (get back to the terminal) by: 
> docker run -d -p 4000:80 friendlyhello

To push this up to the local registry (similar to committing and tag the commit): 
> docker tag friendlyhello localhost:5000/friendlyhello  
> docker push localhost:5000/friendlyhello  

Note: pushing may take a couple of minutes with the size of the docker registry.

From there it's possible to stop the running container and remove the images
> docker container ls  
> docker container stop ${CONTAINER ID}   
> docker image remove friendlyhello  
> docker image remove localhost:5000/friendlyhello  

It's easy to pull the image back now and use it again or just b y running it the image will be pulled
> docker pull localhost:5000/friendlyhello  
> docker run -d -p 4000:80 localhost:5000/friendlyhello   

#Swarm
To run this with high availability as a swarm:
> docker stack deploy -c docker-compose.yml friendlyhelloswarm

This will bring up container with a visualizer and redis cache. 
You should now be able to reach the container on localhost (port 80 which is default) and you can see a visual representation of the containers on localhost:8080

