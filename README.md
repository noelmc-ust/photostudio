# Dockerization and Deployment of the PhotoStudio App

## Dockerfile
First we need to create the dockerfile for the app . since we are using a NodeJS Server our docker file should be like this

```
FROM node
WORKDIR /app
COPY package*.json /app/
RUN npm install
COPY . /app/
EXPOSE 3000
CMD ["npm","start"]
```

1. we are installing the node docker image
2. we set the working directory of our app
3. to install the dependency we copy the package.json and package.lock.json file into the working directory
4. running npm install to install the dependencies
5. copying our whole source code into the working directory
6. since our express server is running at 3000 we expose it
7. Then we make sure the server is started by running npm start using CMD - beacuse it has default executing power over other commands


        Dont forget to add .dockerignore file to avoid unenecssary files while creating image

## Image and Container Creation

We clone our git repo into the EC2 instance and from there we go into the cloned repo and run the docker builc command to create image of that project
```
docker build -t <name> <location of docker file>
```
after sucessfully creating the image we need to create the container so we run the docker run command to crrate it in daemon mode (so app runs in background, dosent exit when we exit the container)

```
docker run -td --name <name of app> -p <host:3000> <image name>
```
```
http://13.127.6.204:83 - App is hosted in this link
```
after creating the container we need can check if the app is working the web

## Pushin the image into docker hub

First we need to tag our image 
```
docker tag <image name> <username/new image name>
```

after tagging it we push it into the docker hub
```
docker push <new image name>
(find it by running docker ps)
```
```
https://hub.docker.com/repository/docker/nmc9812/studio - docker image link
```

