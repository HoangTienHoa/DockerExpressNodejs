# DockerExpressNodejs
A demo for using docker to deploy NodeJS Project

# Explain Dockerfile
````
FROM node:14.17.0-alpine
    From the base image node, with the version 14.17.0 and alpine variant.
WORKDIR /app
    The directory called app is going to hold our project. If the directory specified doesn’t exist in the image, it is newly created.
COPY package*.json ./
    We are adding our package.json and package-lock.json to our workdir.
RUN npm install
    This command installs the dependencies mentioned in our package.json
COPY index.js ./
    Adds index.js from our app to the image.
CMD [ "node", "index.js"]
    Executes node index.js
````
# Build image and Run container
Case 1
````
    $ docker build -t docker-express-app .
		-t docker-express-app: the name for the image along with its tag, here, we leave the tag to be default (latest). (-t option is used to specify a name and a tag for the image to be built)
		. :the Dockerfile in the current directory, using which the image is built.

	$ docker images
	$ docker run --name express-api -d -p 4000:4000 docker-express-app
		--name express-api: naming our container with --name option, express-api is the name given.
		-d: to run our app in detached mode.
		-p 4000:4000 : -p option is to map a port to our image, here we are mapping the port 4000 of our localhost to the port 4000 of our container.
		docker-express-app: the image to run
	$ docker ps
	-> Now you can test http://localhost:4000/
	
	
	Stop/Start image instance
	$ docker stop express-api
		STOP INSTANCE
	$ docker start express-api
		START INSTANCE	
		
	Delete comtainer and image which is not use.
	$ docker stop express-api
	$ docker rm comtainerID
	$ docker rmi imageID
````
Case 2
    $ docker-compose up
# Testing
    http://localhost:4000/

# Ref
    https://medium.com/featurepreneur/a-guide-to-dockerize-your-node-js-application-c24b5e129995
