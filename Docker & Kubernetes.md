
# Section 1

NOTE: Install the Docker extension in CS Code.

Create a file with the contents below and name it `Dockerfile` (without an extension).

```Dockerfile
# This instruction essentially says, "use Node.js as a base image, so that it will be available inside the container."
FROM node:14

# Establish a directory within the file system where the application will run.
WORKDIR /app

# Copy the package.json file into the app directory
COPY package.json .

# run npm install (from the working directory), which will reference the package.json file to install dependencies.
RUN npm install

# Copy the rest of the files into the working directory.
COPY . .

# Expose the container's port 3000 to the outside world because that's the port that node will be listening on for incoming requests.
EXPOSE 3000

# Run the application with the node command, which is available because we installed it above.
CMD [ "node", "app.mjs" ]
```

### Run the above file
This will build an image which can be started as a container.
```console
docker build .
```
 
 #### The output should look something like this:
 ![[Screenshot 2024-03-22 at 8.19.27 PM.png]]

### Run the container 
- The ID of the resulting image file is underlined underlined in the screenshot above.
- We can run a container based on the image with the `docker run` command.
- Once an image is created, it can be run from anywhere.
```console
docker run e075c847b1f6
```
- We need to publish the port we want to expose when running the container
	- Add `-p 3000:3000` to expose 'computer' port 3000 on container port 3000, which means use localhost's port 3000 to access the container's port 3000.
	- By default, there is no connection between the container and our host operating system.
	- E.g., if we want to make HTTP requests, we need to open the port on which we want to communicate.
```console
docker run -p <localhost port>:<container port> <container name or ID>
docker run -p 3000:3000 e075c847b1f6
```
### Stop the container
- While a container is running, run `docker ps` to list all running containers.
- Copy the name of the container to stop.
- Run `docker stop <container name>`

# Section 2

- hub.docker.com - find images shared by the community

Official images may be pulled and run using the following command (which uses node.js, which is hosted on https://hub.docker.com/_/node, as an example official image):
```console
docker run node
```
- The `docker run` command will fail at first because node will not be found locally, but then docker will pull the node image from docker hub.

List all docker images, regardless of whether they are running or not:
``` console
docker ps -a
```

Run the container and ==expose== an interactive session from inside the container.
- This will start the Node.js REPL.
- This is nice to get started, but not a common use-case.
```console
docker run -it node
```

Run an Alpine linux container, ==expose== an interactive session from inside the container,  and install Python on it:
- Note that the Python installation will not persist, it will need to be reinstalled, when running the container again.
```console
docker run -it alpine
apk add --no-cache python3 py3-pip
```


Sample Dockerfile (See expanded version of this sample below):
```Dockerfile
FROM node
WORKDIR /app
COPY . /app
RUN npm install
EXPOSE 80
CMD ["node", "server.js"]
```

The same sample Dockerfile as above, but with comments:
```Dockerfile
# Enter the name of an image that exists locaolly or on docker hub.
# Once you pull an image the first time, it will be cached locally for future uses.
FROM node
  
# The default working directory normally points to the root folder.
# This assigns the /app folder as the default working directory of the container.
WORKDIR /app

# Pull files and folders from the source image above and place them in the
# working directory of the container.
# The ". ." specify the source path and destination path.
# The first "." tells docker to copy all the files and folders in the folder
# that contains the Dockerfile (excluding the Dockerfile) into the image.
# The second "." tells docker where those copied files and folders should be 
# stored within the image.
# Every image has its own file system
# COPY . .

# It's good practice to Not use the image's root folder as the working directory,
# but to use a subfolder (having any name) within root
# COPY . /app

# Because we assigned /app as the default working directory to offset the
# working directory from the root folder, we ~can~ point the default working
# directory as the destination.
# COPY . .

# Although it isn't necessary to explicitly call out the /app folder,
# using an absolute path is easier to debug because we don't need to
# double check what the working directory is set to.
# NOTE: This is Max's preference, but I'm not sure about repeating the path 
# everywhere.
COPY . /app
  
# Tell Docker to run a command to install depenencies
RUN npm install
  
# Expose a container's port to our local machine.
# Technically, it may not be necessary to expose port 80 here, 
# but it is required to publish the port number when running the container.
# It's good practice to document the EXPOSEd port in the Dockerfile.
EXPOSE 80

# Start the server
# ---------------------------------------------------------------------------
# 'RUN node server.js' will not work because this command will run while 
# building the image.
#
# An image is a template for a container. The image is not what we run,
# we run a container BASED ON an image, so the command 'RUN node server.js' will
# run on the image (i.e., on the template), which is not what we want.
#
# We want all the dependencies and code in the template, but we only want to
# start a server upon starting a container that is based on the image.
# Also, if we start multiple containers based on the same image, we want
# to start multiple servers
#
# CMD
# This command will not run when an image is created, but will run
# in the container when the container starts.
# The CMD arguments need to be passed as an array of strings.
# The image file's default CMD will be used if this line isn't specified.
# In that case, if image file's default CMD doesn't exist, you'll get an error.
CMD ["node", "server.js"]

# CMD SHOULD ALWAYS BE THE LAST INSTRUCTION IN A DOCKERFILE!!!
```

### Build a new custom image based on a docker file
- Command: `docker build <path to Dockerfile>`
- Using "." as the path tells the docker build command the Dockerfile is in the current directory.
```console
docker build .
```

### Run the container
- The -p flag is for 'publishing' a port.
- The -p format is "`<local computer port number>`:`<container port number>`"
	- E.g., in a browser, localhost:`<local computer port number>` would make an HTTP request to the container via port `<container port number>`.

```console
docker run -p 3000:80 e075c847b1f6
```

### Images are Read-Only
- You need to **rebuild** to copy changes into an image.

### Understanding Image Layers
- By using layer-based images, only instructions that change, and subsequent instructions, are reevaluated.
- In a layer-based architecture:
	- When you build an image, Docker caches every Dockerfile instruction result.
	- When you rebuild, Docker uses a cached result if there's no need to rerun an instruction.
- When you run a container based on an image, the container essentially adds another layer on top of the image layers (this is the result of running the CMD instruction, assuming CMD is the last instruction in your Dockerfile).

#### Image Layer Optimization for Dependencies

If the `npm install` instruction comes after copying source code into an image, then the install instruction will need to run every time that we copy changes to source code into the image when building.
Instead, copy the `package.json` file into the image and run `npm install` before copying the source code into the image. When building, only instructions after installing npm dependencies will need to run.

```Dockerfile
FROM node
WORKDIR /app
# Dependencies are copied & installed.
# These steps won't run again unless ther's a change to package.json.
COPY package.json /app
RUN npm install
# Sorce code is copied into image.
COPY . /app
EXPOSE 80
CMD ["node", "server.js"]
```


### Containers do not copy over code and environment from images into new files within the containers!
### Containers use the environment stored with images and add a layer on top of the image layers.
	For example, resources (e.g., memory) would be allocated to a node server process and an application, but the code for the application code and node environment itself is not copied for each instance. If we have 1 image and 1 containers, the code and environment exists once inside the image, and the containers then use the image and code.

### Managing Images & Containers


Restart and Stop a container:
```console
docker start <container ID>
docker stop <container ID>
```
### Understanding Attached & Detached Containers

"Attached" means that "we are" listening to the **output** (STDOUT) of the container (e.g., outputting to the console.)
##### NOTE: Attaching doesn't mean that we are also able to send inputs to STDIN.

Use the `-d` flag to run a new container in detached mode, so that it  doesn't block a terminal:
```console
docker run -p 8000:80 -d <image ID>
```

Run a container again in detached mode:
```console
docker container attach <container name or ID>
```

Attach a running container to get its output via the `attach` or `logs`:
	`docker logs -f` will also output past logs that were missed while in detached mode.
```console
docker start -1 <container name or ID>
docker attach <container name or ID> 
docker logs -f <container name or ID>
```

While in detached mode, we can retrieve the past logs that were printed by a container (i.e., the ones we missed because we were in detached mode):
```console
docker logs <container name or ID>
```


### Entering Interactive Mode

Run the following Python code in a Python container

```python
# Filename: rng.py
from random import randint
min_number = int(input("Enter the min number: "))
max_number = int(input("Enter the max number: "))
if (max_number < min_number):
	print("Invalid input. Shutting down)
else:
	rnd_number = randint(min_number, max_number)
	print(rnd_number)
```

```Dockerfile
# An official python image will be downloaded from dockerhub
FROM python
WORKDIR /app
COPY . /app
CMD ["python", "rng.py"]
```

The Python script in the container that is running the above image will crash because an input isn't attached -- the script won't find anything connected to receive input from the STDIN, so it will crash.

You'll need to add a `-i` flag to launch the container in interactive mode. Adding a `-t` flag to allocate a pseudo-TTY, in addition to the `-i` flag, will essentially create a terminal for user input that would be routed to the STDIN. 
Note: `-it` is equivalent to `-i` and `-t`.
Note: `-t` will be remembered the next time a container runs.
```console
docker build .
docker run -it <image name or ID>
```

The container will shut down after the script ends.

`docker start -a <image name or ID>` will run in attached mode, but will only take a first input and it will act strangely thereafter.

`docker start -a -i <image name or ID>` will run in attached mode and input mode.


### Deleting Images and Containers

#### Removing Containers:
```console
docker ps
docker stop <container name or ID 1> <container name or ID 2> ...
docker rm <container name or ID 1> <container name or ID 2> ...
```
#### Remove all stopped containers:
```console
docker container prune
```
#### Removing Images:
- An image must not be in use by any containers to remove it.
- The removal of each layer of each image is listed as it is removed.
```console
docker images
docker rmi <image name or ID 1> <image name or ID 2> ...
```

#### Remove all images (including tagged images):
See below for information about tags.
```console
docker image prune -a
```

#### Automatically remove container when it stops
	This is useful during development, when you'll need to stop a container when code changes.
```console
docker run -p 8000:80 -d --rm <image name or ID>
```


### Inspecting Images

#### Display detailed information on one or more images
Note: You can also inspect the layers within the detailed information.

```console
docker image inspect <image name or ID>
```

### Copying Files Into & From a Container

#### Copying into a Container
```console
docker run <container name or ID>

docker cp <source folder name>/<file name> <container name or ID>:/<path to destination folder>
docker cp <source folder name>/. <container name or ID>:/<path to folder>
```
#### Copying from a Container
Useful for things like retrieving log files.
```console
docker <container name or ID>:/<path to source folder> <destination folder name>
docker <container name or ID>:/<path to source file> <destination folder name>
```

### Naming & Tagging Containers and Images
```console
docker build -t <image name>:<(optional) image tag to indicate version> .
docker build -t fancy_image:latest .

docker run --name <desired name for container>
```

#### Rename an image
```console
docker tag <old image name> <new image name>
docker tag <old image name>:<tag> <new image name>:<tag>
docker tag <old image name>:<tag> <new image name>:
```

Note: Renaming an image doesn't remove the original image.

### Pushing Images to DockerHub or Private Registry

#### DockerHub
Share: `docker push <image name>`
Use: `docker pull <image name>`

Private Registry
Share: `docker push <host>:<image name>`
Use: `docker pull <host>:<image name>`

Build an image with the name of the repository (i.e., image name) you plan to use:
`docker build -t <dockerhub account>/<image name>`


## Managing Data & Working with Volumes

### Kinds of Data
- **Application**: (E.g., Code + Environment)
	- Written by you
	- Added to image and container in build 
	- Fixed -- can't be changed after image is built.
	- Read-Only, hence stored in images
- **Temporary App Data**: (E.g., Entered user inputs)
	- Fetched/Produced in running container
	- Stored in memory
	- Read + Write, hence stored in containers
- Permanent App **Data**: (E.g., User Accounts)
	- Fetched/Produced in running container
	- Stored in files or a database
	- Must not be lost if container stops/restarts
	- Read + Write, Permanent, stored with Containers & Volumes

#### Types of Data Storage
- Volumes (Managed by Docker)
	- Docker sets up and maps a path within a container to a folder/path on your localhost.
	- The location of the folder/path is unknown to you (= dev).
	- Managed via `docker volume` commands.
	- Types of Volumes:
		- Anonymous Volumes
			- Data is only accessible while the corresponding container exists, but it survives container shutdown and restarts.
			- If you run with `--rm`, then the volume is deleted when the container stops.
			- If you run without `--rm`, then a new anon. volume is created each time we run an image and the old anon. volume becomes inaccessible to the new container.
			- Useful for locking in data which already exists in a container and that shouldn't be overwritten by bind mount data (see below) (e.g., to prevent containers' node_modules or temp files from being overwritten with local machine files).
			- (Volume Creation Option 1) Add to Dockerfile:
				- `VOLUME ["<path inside container from root>"]`
				- NOTE: You must use option 2 to override read-only access to bind mounts in parent folders (see below for more information about bind mounts).
			- (Volume Creation Option 2) Add to the `docker run` command:
				- `docker run -v <path inside container from root> <image name or ID to use>:<(optional) image tag>`
				- e.g., `docker run --name feedback-app -v /app/feedback feedback-node:volumes`
		- Named Volumes
			- Data persists after container stops.
			- Add to `docker run` command:
				- `docker run -v <custom volume name>:<path inside container from root> <image name or ID to use>:<(optional) image tag>`
				- e.g., `docker run -d -p 3000:80 --rm --name feedback-app -v feedback:/app/feedback feedback-node:volumes`
			- Can be shared by multiple containers to share data between containers.
	- Clear unused anonymous volumes:
		- `docker volume rm <volume name>`
		- `docker volume prune`
- Bind Mounts (Managed by You)
	- ### Bind mounts are for devlopment, not for production, because source file on you host machine will not be available when you deploy a container!!!
	- Useful for development. Changes to source code files on localhost that are at bind mounts would be reflected within containers.
	- The folder/path on you machine is specified.
	- Great for persistent data that is editable by you.
		- Source code can be stored in bind mounts so that containers could have access to the latest code.
		- Data can be shared among containers.
	- Add to `docker run` command:
		- `docker run -v <custom volume name>:<path inside container from root> -v <absolute path to a folder (or file) on host machine>:<path inside container from root (aka the 'map path')> <container name or ID>`
	- **NOTE**: BY DEFAULT, BIND MOUNT VOLUMES CAN WRITE TO THE LOCAL HOST VOLUMES!!!
		- Add `:ro` after the bind map path to set the local host path to READ-ONLY.
		- You may need to allow write access to a `temp` folder so that 
			- E.g., `docker run -v <custom volume name>:<path inside container from root> -v "<local absolute path>:<map path>:ro" -v /app/temp <container name or ID>`
	- **Note**: if either path contains spaces or special characters, the absolute path and the map path must be placed together inside a single set of quotes .
	- Shorthand for absolute paths in `docker run` commands:
		- **macOS / Linux**: `-v $(pwd):/app`
			- E.g., `docker run -d -p 3000:80 --rm --name feedback-app -v feedback:/app/feedback -v $(pwd):/app feedback-node:volumes
		- **Windows**: `-v "%cd%":/app`
		- NOTE: if there are spaces or special characters in the expanded `pwd` path or map path, then the `pwd` command and the map path will again need to be in quotes: E.g., `-v "$(pwd):/app"`
	- Docker evaluates all volumes being configured in instructions; and if there are clashes, the instructions with longer internal paths win.
		- In the following sample instruction, the `/app/node_modules` directory will not mirror the local node_modules folder because the anonymous volume path (/app/node_modules) is deeper than the bind mount path (/app) (I.e., the local `/app/node_modules` folder will be ignored): 
			- `docker run -d -p 3000:80 --rm --name feedback-app -v feedback:/app/feedback -v $(pwd):/app -v /app/node_modules feedback-node:volumes`
	- Make sure Docker has access to the folder you're sharing as a bind mount.
		- Go to the Docker app's preferences --> Resources -- > File Sharing
			- The absolute path you want to share (or one of the absolute path's parent folders) should be listed on the File Sharing page.
	- The Bind Mount data survives a container shutdown and container deletion, so the data would still need to be deleted from a host machine after deleting an associated container(s).
### TL;DR
- Anonymous Volume
	- `docker run -v /app/data`
- Named Volume
	- `docker run -v volume_name:/app/data`
- Bind Volume
	- `docker run -v /local/path/to/code:/app/data` (READ/WRITE)
	- `docker run -v /local/path/to/code:/app/data:ro` (READ-ONLY)
#### Specify a Volume for Storing Persistent Data
- A volume is location on the local host that a container can access to read or write persistent data.
- Volumes must be specified while building the image.

```Dockerfile
FROM node
WORKDIR /app
COPY package.json .
RUN npm install
# When using bind mounts during development COPY won't be necessary, but it will be needed for production.
COPY . .
EXPOSE 80
# Anonymous Volume
# Docker will map data the container writes to /app/feedback to the localhost.
# This is a path inside the container
# An anonymous volume can be specified in the run command as
# an alternative to adding this VOLUME instruction here.
VOLUME ["/app/feedback"]
CMD ["node", "server.js"]
```

## Getting Started with Bind Mounts

https://headsigned.com/posts/mounting-docker-volumes-with-docker-toolbox-for-windows/

#### Debugging
- Remove `--rm` flag from run command so that we can get **LOGS** from a running container.


### NodeJS + `nodemon`
- Changes to JS files will normally not take effect unless you restart a container based on updated files.  The `nodemon` package has a file change watcher, so if it is added as a development dependency, then the package will load changes to JS files as they are saved (the browser would still need to reload).
#### To add `nodemon` to the Development Dependencies:
- Add a `devDependencies` section to the package.json file, and add `nodemon` as a dependency.
- Add a `scripts` section to start the `nodemon` server instead of node.
- Change the `Dockerfile` to run `npm start` instead of `node server.js`
- ##### Debugging:
	- Add a `console.log()` message in the `server.js` file after running a container.
	- Check if `nodemon` loaded the change by running a `docker log <container name/ID>` command.
		- NOTE: yellow text is from when the server starts and green text indicates logs from when the server restarted.
```package.json
{
	"name": "data-volume-example",
	.
	.
	.,
	"scripts": {
		"start": "nodemon server.js"
	},
	"dependencies": {
		"body-parser": "^1.19.0",
		"nodemon": "^4.17.1"
	},
	"devDependencies": {
		"nodemon": "2.0.4"
	}
}
```

```Dockerfile
FROM node:14
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
EXPOSE 80
# CMD [ "node", "server.js" ]
CMD [ "npm", "start" ]
```

#### .dockerignore
- Tells the COPY instruction which files/directories on the host to ignore when copying to an image.
- create a file called `.dockerignore` in the root project folder, and add each file or folder to ignore as lines in the file (similar to a `.gitignore` file.)

Sample `.dockerignore` file (ignores the Dockerfile and .git file when building):
```.dockerignore
Dockerfile
.git
```

### ARG & ENV Variables
- DON'T INCLUDE SENSITIVE DATA DIRECTLY IN A `Dockerfile`!!!
	- Values are "baked into the image" and everyone can read these values via `docker history <image>`.
- DON'T COMMIT ENV/ARG FILES WITH SENSITIVE DATA TO A SOURCE CONTROL REPO!!!
- Use a separate environment variables file which is then only used at runtime (i.e. when you run your container with `docker run`).
- **Place toward the end of your Dockerfile to prevent rebuilding layers.**
#### ARG
- `--build-arg`
- Build-time ARGuments
#### ENV
- Docker can set environmental variables, which applications, such as Node, can retrieve.
- Environmental variables may be set in a Dockerfile or in the run command via the `--env` flag.
- Use Case: **__We won't need to rebuild__** an image just to change the port if the port is specified as an environmental variable.
- Runt-time ENVironmental variables

```console
/* --env specifies an environmental variable in the console.  /*
docker run -p 3000:8000 --env PORT:8000 image_name:tag_name
```

```Dockerfile
FROM node:14
.
.
.
# Create (or "Announce") an environmental variable and set it to 80
# NOTE: PORT is now a recognized variable that can be
#       used in the rest of the Dockerfile
#.      (with a $ before the variable name).
# NOTE: Capital letters is optional.
ENV PORT 80

# Expose looks up the PORT Variable by adding a $ before the vaiable.
EXPOSE $PORT
.
.
.
```

```server.js
/// Node Server Code

//app.listen(80)

// Tell Node to look up the globally available environmental
// variable for the 'PORT' variable using the dotenv module.
app.listen(process.env.PORT)

```

### Environmental Variables File
- As an alternative to specifying environmental variables in the Dockerfile or command line, a file may list environmental variables.
- The file is typically named  `.env`, but it can be named anything.
- 
Example use of an environmental variables file:
```.env
PORT=8000
```

```console
/* The .env file is in the same folder from which we are running this instruction /*
docker run -p 3000:8000 --env-file ./.env image_name:tag_name
```



> [!Environment Variables & Security]
> One important note about **environment variables and security**: Depending on which kind of data you're storing in your environment variables, you might not want to include the secure data directly in your `Dockerfile`.
> 
> Instead, go for a separate environment variables file which is then only used at runtime (i.e. when you run your container with `docker run`).
> 
> Otherwise, the values are "baked into the image" and everyone can read these values via `docker history <image>`.
> 
> For some values, this might not matter but for credentials, private keys etc. you definitely want to avoid that!
> 
> If you use a separate file, the values are not part of the image since you point at that file when you run `docker run`. But make sure you don't commit that separate file as part of your source control repository, if you're using source control.

## Using Build Arguments

### A Dockerfile having a Default Build Argument
```dockerfile
FROM node:14
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
# Specify arguments just before you need them
# to prevent rebuilding layers.
ARG DEFAULT_PORT=80
ENV PORT $DEFAULT_PORT
EXPOSE $PORT
...
# Assuming we're running nodemon for development 
# (i.e., we're not running `node server.js`.)
CMD [ "npm", "start" ]
```
### The port will be set to 80 because it isn't specified
```console
docker build -t feedback-node:web-app .
```
### The port will be set to 8000 because it is specified in the command
```console
docker build -t feedback-node:dev --build-arg DEFAULT_PORT=8000 .
```



# Section 4 - Networking - (Cross-)Container Communication

- Communication with the internet should just work "out of the box" for any container.
	- E.g., GET and POST requests to online web APIs should work.
- Communication with services, or other containers, running on your local machine will not work without configuration.


### Container to Host Communication

#### `localhost` vs `host.docker.internal`

`host.docker.internal` is a domain that is recognized by Docker and is understood as the IP address of the localhost (that the container is running on) as seen from inside the container.

```js
const express = require('express');
const mongoose = require("mongoose");

// Assume MongoDB is running on the local machine, 
// but outside of the container.
mongoose.connect(
	// Trying to reach Mogno via 'localhost' won't work, building will crash
	// because localhost is unreachable.
	//'mongodb://localhost:27017/swfavorites',
	
	// Replace 'localhost' with a URL that Docker recognizes.
	// NOTE 27017 is the default MongoDB port
	'mongodb://host.docker.internal:27017/swfavorites',
	{ useNewUrlParser: true },
	(err) => {
		if (err) {
			console.log(err);
		} else {
			app.listen(3000);
		}
	}
);
```

### Container to Container Communication


Get the container's IP Address with `docker inspect`:
- Th `IPAddress` will be under `NetworkSettings`.
```console
docker run -d --name mongodb mongo
docker inspect mongodb
```

```js
const express = require('express');
const mongoose = require("mongoose");

// Assume MongoDB is running in another container.
// Assume the Mongo container's IP Address is 172.17.0.2.
mongoose.connect(
	// Replace 'localhost' with the Mongo conatiner's IP Address.
	'mongodb://172.17.0.2:27017/swfavorites',
	{ useNewUrlParser: true },
	(err) => {
		if (err) {
			console.log(err);
		} else {
			app.listen(3000);
		}
	}
);
```


### Docker Container Networks

1. Create a network with `docker network create <network name>`
2. Specify the same network name, with the `--network` flag, when running containers.
3. Specify the name of the first, or previous, container connected to the network as the domain in your code before running subsequent containers.
4. No need to publish ports with the `-p` flag when running containers for containers to communicate with each other.
5. The `-p` flag is still required if connecting from the localhost from outside the container.

```console
docker network create favorites-net
docker run -d --name mongodb --network favorites-net mongo
docker run -d --name favorites --network favorites-net -d --rm -p 3000:3000 favorites-node
```

```js
const express = require('express');
const mongoose = require("mongoose");

// Assume MongoDB is running in another container, called 'mongodb'.
// Assume the Mongo container was already added to a container network.
mongoose.connect(
	// Replace 'localhost' with the name of a conatiner that is already on the container network (In this case `mongodb).
	'mongodb://mongodb:27017/swfavorites',
	{ useNewUrlParser: true },
	(err) => {
		if (err) {
			console.log(err);
		} else {
			app.listen(3000);
		}
	}
);
```

List Docker Networks
- `docker network ls`

> [!NOTE] Docker Network Drivers (Module/Section 77)
> Docker Networks actually support different kinds of "**Drivers**" which influence the behavior of the Network.
>
> The default driver is the "**bridge**" driver - it provides the behavior shown in this module (i.e. Containers can find each other by name if they are in the same Network).
>
>The driver can be set when a Network is created, simply by adding the `--driver` option.
>
>```console
docker network create --driver bridge my-net
>```
>
>Of course, if you want to use the "bridge" driver, you can simply omit the entire option since "bridge" is the default anyway.
>
>Docker also supports these alternative drivers - though you will use the "bridge" driver in most cases:
>
>- **host**: For standalone containers, isolation between container and host system is removed (i.e. they share localhost as a network)
  >  
>- **overlay**: Multiple Docker daemons (i.e. Docker running on different machines) are able to connect with each other. Only works in "Swarm" mode which is a dated / almost deprecated way of connecting multiple containers
 >   
>- **macvlan**: You can set a custom MAC address to a container - this address can then be used for communication with that container
 >   
>- **none**: All networking is disabled.
  >  
>- **Third-party plugins**: You can install third-party plugins which then may add all kinds of behaviors and functionalities
> 
> As mentioned, the "**bridge**" driver makes most sense in the vast majority of scenarios.


## Section 5: Building Multi-Container Applications with Docker

Reminders
- Run `docker container prune` to make sure you don't have old containers running that your browser may connect to when testing.
- Run `docker image prune -a` to remove unused images.

### Use system's localhost network as the network for containers
- Use `host.docker.internal` as the IP address to connect to the localhost network.
```console
docker run --name mongodb --rm -d -p 27017:27017 mongo

cd backend
sudo docker build -t goals-node .
docker run --name goals-backend --rm -d -p 80:80 goals-node

cd ../frontend
sudo docker build -t goals-react .
docker run --name goals-frontend --rm -d -p 3000:3000 goals-react
```

### Use a Docker Network
- NOTE: Your local machine won't be able to communicate with the Mongo container through the Docker network because its port isn't published in the run command, but the other containers will be able to communicate with it because they're on the same Docker network.
- In JS code, use container names in place of target container's IP addresses or 'localhost' (assuming the code doesn't execute on the browser, as ReactJS does).
- The ReactJS frontend container doesn't need to be on the same network because it will connect to the backend's port 80, which is exposed.
- We're using a named volume to persist Mongo data with `-v data:/data/db`, which will create a named `data` volume that persists data stored in the Mongo container's`/data/db` directory.
- PASS ENVIRONMENTAL VARIABLES AS THE USERNAME AND PASSWORD IN THE TERMINAL BECAUSE TERMINAL COMMANDS ARE LOGGED AND AGAIN IN THE BACKEND FILE BECAUSE THE CODE WILL BE AVAILABLE IN A CODE REPO!!!
	- `docker run --name some-mongo -e MONGO_INITDB_ROOT_PASSWORD_FILE=/run/secrets/mongo-root -d mongo`

```js
mongoose.connect(
	/// USE host.docker.internal IF USING THE SYSTEM'S 
	/// LOCALHOST NETWORK INSTEAD OF A DOCKER NETWORK
	//'mongodb://host.docker.internal:27017/course-goals',
	
	/// USE CONTAINER NAMES IF USING A DOCKER NETWORK
	//'mongodb://mongodb-container:27017/course-goals',

	/// Docker Network Container name + Mongo Username & Password
	'mongodb://myusername:mypassword@mongodb-container:27017/course-goals?authSource=admin',
	{
		useNewUrlParser: true,
		useUnifiedTopology: true,
	},
	(err) => {
		if (err) {
			console.error('FAILED TO CONNECT TO MONGODB');
			console.error(err);
		} else {
			console.log('CONNECTED TO MONGODB');
			app.listen(80);
		}
	}
);
```

```js
// (Portion of) ReactJS Frontend Code

async function fetchData() {
	setIsLoading(true);
	try {
		/// ReactJS runs in a browser, so don't use
		/// the target container name here.
		const response = await fetch('http://localhost/goals');
		
		/// We would normally replace 'localhost' with the
		/// target container, 'goals-node'.
		//const response = await fetch('http://goals-node/goals');
		
		const resData = await response.json();
		if (!response.ok) {
			throw new Error(resData.message || 'Fetching the goals failed.');
		}
		setLoadedGoals(resData.goals);
	} catch (err) {
		setError(
			err.message ||
			'Fetching goals failed - the server responsed with an error.'
		);
	}
	setIsLoading(false);
}
```


Reminders: 
- The Mongo container below should use a bind mount rather than a named volume to persist data. E.g., `-v /my/own/datadir:/data/db` instead of `-v data:/data/db`.
- To bind an `app` folder in a container to `/Users/username/development/backend` on a local machine, then a bind mount would be created with:
	- `-v /Users/username/development/backend:/app`
- Longer internal paths take precedence over shorter ones, so:
	- `/app/logs` inside the container are not overwritten by logs on the host machine.
	- `-v /app/node_modules` inside the container is not overwritten by files on the host machine.

```console
docker network create network-name

docker run --name mongodb-container \
	--rm -d \
	-v data:/data/db \
	--network network-name \
	-e MONGO_INITDB_ROOT_USERNAME=myusername \
	-e MONGO_INITDB_ROOT_PASSWORD=mypassword \
	mongo

cd backend
echo use sudo to build on MacOS
sudo docker build -t goals-node .
echo Creates a bind mount for code that persists container teardown and 
echo allows for live source code updates.
echo Creates a named volume for logs that persists container teardown.
docker run --name goals-backend \
	--rm -d \
	-v /Users/username/development/backend:/app \
	-v logs:/app/logs \
	-v /app/node_modules \
	--network network-name \
	-p 80:80 \
	goals-node

cd ../frontend
echo use sudo to build on MacOS
sudo docker build -t goals-react .
docker run --name goals-frontend \
	--rm -d \
	-p 3000:3000 \
	goals-react
```



#### NOTE: Mongo has changed since the course was released. If you get the following authentication error when trying to connect to Mongo from the backend,

Error message:
```console
FAILED TO CONNECT TO MONGODB
MongoError: Authentication failed.
    ... {
  ok: 0,
  code: 18,
  codeName: 'AuthenticationFailed'
```

#### try one of the following:

1. Specify "mongo:5" in the Mongo Dockerfile.

2. Create user in the admin database by setting an additional environmental variable, `MONGO_INITDB_DATABASE`.
```console
docker run --name mongodb-container \
	--rm -d \
	-v data:/data/db \
	--network network-name \
	-e MONGO_INITDB_DATABASE=admin \ # Create user in the admin database
	-e MONGO_INITDB_ROOT_USERNAME=myusername \
	-e MONGO_INITDB_ROOT_PASSWORD=mypassword \
	mongo
```

3. Set the `MONGO_USERDB_ADMIN_USERNAME` and `MONGO_USERDB_ADMIN_PASSWORD` in the `docker run` command when running mongo, instead of setting `MONGO_INITDB_ROOT_USERNAME` and  `MONGO_INITDB_ROOT_PASSWORD` as follows:
```console
docker run --name mongodb-container \
	--rm -d \ -v data:/data/db \
	--network network-name \
	-e MONGO_USERDB_ADMIN_USERNAME=myusername \
	-e MONGO_USERDB_ADMIN_PASSWORD=mypassword \
	mongo
```

4. Manually add user credentials and roles in the running Mongo container by running `mongosh` in the container and calling db.createUser() within the mongo shell as follows:

Linux Terminal
```console
docker exec -it mongodb-container mongosh
```

Mongo Shell
```mongosh
use admin;
db.createUser({
  user: "myusername",
  pwd: "mypassword",
  roles: [{ role: "root", db: "admin" }]
});
exit
```


### Section 88: Volumes, Bind Mounts & Polishing for the NodeJS Container

```Dockerfile
# goals-backend Container's Dockerfile
FROM node:14
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
EXPOSE 80
CMD [ "node", "app.js" ]
```

```console
docker run --name goals-backend \
	--rm -d \
	-v /Users/username/development/backend:/app \
	-v logs:/app/logs \
	-v /app/node_modules \
	--network network-name \
	-p 80:80 \
	goals-node
```

When running the goals-backend container, the application won't reload whenever the source code changes.
Add `nodemon` to the development dependencies in `package.json` to automatically reload the NodeJS server upon source code changes:
```json
{
	...
	"scripts": {
		"start": "nodemon app.js"
	},
	...
	"devDependencies": {
		"nodemon": "^2.0.4"
	}
}
```

```Dockerfile
# goals-backend Container's Dockerfile for use with nodemon
FROM node:14
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
EXPOSE 80

ENV MONGODB_USERNAME=root
ENV MONGODB_PASSWORD=secret
# npm start will run nodemon via a script in the package.json file.
CMD [ "npm", "start" ]
```

```js
import dotenv from 'dotenv';
dotenv.config();

mongoose.connect(
	`mongodb://${process.env.MONGODB_USERNAME}:${process.env.MONGODB_PASSWORD}@mongodb-container:27017/course-goals?authSource=admin`,
	{
		useNewUrlParser: true,
		useUnifiedTopology: true,
	},
	(err) => {
		if (err) {
			console.error('FAILED TO CONNECT TO MONGODB');
			console.error(err);
		} else {
			console.log('CONNECTED TO MONGODB');
			app.listen(80);
		}
	}
);
```
#### `-e MONGODB_USERNAME=myusername` will override `ENV MONGODB_USERNAME=root`.
```console
docker run --name goals-backend \
	--rm -d \
	-v /Users/username/development/backend:/app \
	-v logs:/app/logs \
	-v /app/node_modules \
	--network network-name \
	-e MONGODB_USERNAME=myusername
	-p 80:80 \
	goals-node
```
#### .dockerignore 
- Add to the root folders of the FRONTEND and BACKEND containers.
```.dockerignore
node_modules
Dockerfile
.git
```

```console
docker run --name goals-frontend \
	--rm -d \
	-v /path/to/frontend/src:/app/src \
	-p 3000:3000 \
	-it \
	goals-react
```


## Section 6: Docker Compose: Elegant Multi-Container 

### Compose File Configuration

<ol>
<li>
Create a `docker-compose.yaml` file in the project folder. The file will describe the multi-container environment.
</li>
</ol>
```sh
/app
	/frontend
	/backend
	.gitignore
	docker-compose.yaml
```

<ol>
<li value="2">
Start by defining a Docker Compose Specification `version` on the first line of the file.
</li>
</ol>
<ol>
<li value ="3">
Specify the services (i.e. the containers).
<p>ADD 2 SPACES PER INDENTATION LEVEL</p>
</li>
</ol>
```docker-compose.yaml
version: "3.8"
services:
  mongodb:
  backend:
  frontend:
```

<ol>
<li value=4>
Configure the containers (i.e., the services).
<p>Terminal command implementation (for reference):</p>
</li>
</ol>
```console
docker run --name mongodb-container \
	--rm -d \
	-v data:/data/db \
	--network network-name \
	-e MONGO_INITDB_DATABASE=admin \ # Create user in the admin database
	-e MONGO_INITDB_ROOT_USERNAME=myusername \
	-e MONGO_INITDB_ROOT_PASSWORD=mypassword \
	mongo
```
<ul>
</li>
<ul style="list-style-type: none;">
<li>
Docker Compose implementation:
<p>When you bring services down, they will be removed, so no need for <span style="color: orange;">--rm</span>.</p>
<p>We can specify <span style="color: orange;">-d</span>, for detached mode, when we run a command to start the services together with the docker-compose file.</p>
<p>Add comments with <span style="color: orange;">#</span>.</p>
</li>
</ul>

#### Project File Structure for Examples Below

```plaintext
/project-root
│
├── /frontend
│   ├── Dockerfile
│   ├── package.json
│   ├── package-lock.json
│   ├── README.md
│   └── /public
│       └── index.html
│
├── /backend
│   ├── Dockerfile
│   ├── /css
│   ├── /js
│   ├── /images
│   └── /src
│       ├── /components
│       ├── app.js
│       ├── index.js
│       └── index.css
│
├── /env
│   └── mongo.env
│
├── docker-commands.txt
└── docker-compose.yaml
```

```docker-compose.yaml
version: "3.8" # You don't need to add the version number anymore.

services:
  # docker-compose may assign names that are different from the service names,
  # but you'll still be able to access the services in URLS by referencing
  # the service names listed in this file.
  # The name here is a "Service Name", which defaults to 
  # <project folder name>_<Service Name>_<incrementing number>.
  # You can separately specify a container name with `container_name: <name>`
  mongodb:
    image: 'mongo' # The image will be pulled if not on the system
    
    volumes:
	  - data:/data/db
    # environment:
      # BOTH ALTERNATIVE SYNTAXES WORK TO SET ENV VARIABLES
      # KEY:VALUE pairs don't require a "- " before the list item.
      # MONGO_INITDB_ROOT_USERNAME: myusername
      # MONGO_INITDB_ROOT_USERNAME=myusername
    
    # env_file allows you to move the config out of the docker-compose file.
    env_file:
      # Provide path relative to this docker-compose.yaml file.
	  - ./env/mongo.env
    
    # A network may be specified here, but docker will, by default, create an
    # environment for all the services when using docker-compose and add the
    # services to the network.
    netowrk:
      # E.g. also add to this special network, goals-net, in addition
      # to the one that docker will create.
      - goals-net

  backend:
    # Note images will only be built by docker-compose based on 
    # whether it detects changes that were made in any layers.
    # SHORTHAND FORM BUILD
    # This is the shorthand for setting the build path
    # This assumes the dockerfile name at the path is "Dockerfile".
    # build: ./backend
    
    # LONG FORM BUILD
    build:
      # THIS SERVICE'S IMAGE WILL BE GENERATED FROM THIS PATH
	  context: ./backend
	  # Add the Dockerfile file name. 
      # The backend Dockerfile happens to be named "Dockerfile".
	  dockerfile: Dockerfile
	  # How to specify ARGs, if your dockerfile uses them.
	  # args:
	    # some-arg: 1

    # Specify exposed/published ports:
	ports:
	  - "<host port>:<container internal port>"
	  - "80:80"

    volumes:
      # Named volume
      # Need to be listed again under volumes below.
	  - logs:/app/logs
	  # Bind mount
	  # The host path can be a path relative to docker-compose.yaml.
	  # It doesn't need to be a full path as when using a run command.
	  - ./backend:/app
	  # Anonymous Volume
	  # Doesn't need to be listed again under volumes below.
	  - /app/node_modules

    env_file:
      - ./env/backend.env

    # Specify whether the service (i.e. the container) depends on another
    # service being up and running for this service to run properly.
    depends_on:
      # List the service names that this service depends on.
      - mongodb

  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
    volumes:
      # Bind the source code from the host machine onto the container.
      - ./frontend/src:/app/src

	# Interactive Mode
	# Even if the service is started in detached mode, the service will 
	# be able to receive input and start up correctly.
    # Let service know it needs an input connection (similar to '-i' flag)
    stdin_open: true
    # Let service know it needs to attach a terminal (similar to '-t' flag)
    tty: true

    # We may set the frontend to wait for the backend to start up.
    # (I think) The frontend and backend services should be able to 
    # operate independently for the purpose of modularity.
	depends_on:
	  - backend

# Any named volumes need to be listed again here
volumes:
  # Add the name of the volume followed by a ":" with nothing else.
  data:
  logs:
```


```txt
docker-commands.txt
---------------------
Create Network
---------------------

docker network create goals-net

---------------------
Run MongoDB Container
---------------------

docker run --name mongodb \
  -e MONGO_INITDB_ROOT_USERNAME=max \
  -e MONGO_INITDB_ROOT_PASSWORD=secret \
  -v data:/data/db \
  --rm \
  -d \
  --network goals-net \
  mongo

---------------------
Build Node API Image
---------------------

docker build -t goals-node .

---------------------
Run Node API Container
---------------------

docker run --name goals-backend \
  -e MONGODB_USERNAME=max \
  -e MONGODB_PASSWORD=secret \
  -v logs:/app/logs \
  -v /Users/maximilianschwarzmuller/development/teaching/udemy/docker-complete/backend:/app \
  -v /app/node_modules \
  --rm \
  -d \
  --network goals-net \
  -p 80:80 \
  goals-node

---------------------
Build React SPA Image
---------------------

docker build -t goals-react .

---------------------
Run React SPA Container
---------------------

docker run --name goals-frontend \
  -v /Users/maximilianschwarzmuller/development/teaching/udemy/docker-complete/frontend/src:/app/src \
  --rm \
  -d \
  -p 3000:3000 \
  -it \
  goals-react

---------------------
Stop all Containers
---------------------

docker stop mongodb goals-backend goals-frontend
```


> [!NOTE]
> Installing Docker Compose on Linux
> 
> On macOS and Windows, you should already have Docker Compose installed - it's set up together with Docker there.
> 
> On Linux machines, you need to install it separately.
> 
> These steps should get you there:
> 
> 1. `sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose`
> 
> 2. `sudo chmod +x /usr/local/bin/docker-compose`
> 
> 3. `sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose`
> 
> 4. to verify: `docker-compose --version`
> 
> Also see: [https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/)

Start & Stop Services with Docker Compose
- `docker-compose up`
- `docker-compose up -d` for Detached mode
- `docker-compose down`

While Starting Services, Force Rebuild of images that are built in the docker-compose.yaml file
- `docker-compose up --build`

Build without Starting Services
- `docker-compose build`


## Section 7: Working with "Utility Containers" & Executing Commands In Containers

*Note: The term 'Utility Container' is not an official term. It is used in the course to describe a use-case for containers.*

### Example Utility Container:


### Run a utility-container for development without installing dependencies on your machine.
*The following allows an NPM project to be created without installing Node or NPM packages on the host machine.*
```Dockerfile
FROM node:14-alpine
WORKDIR /app
# That's it...
# Run a container with this image to allow a user
# full control to run commands against this image.

# NOTE The `npm start` CMD below would be overwritten by 
# `npm init` if a command like the following run command was
# executed:
#	`docker run node-util npm init`
#
# CMD ["npm", "start"]

# `npm init` would be appended to the list of commands to
# run after the command(s) specified in the entrypoint.
# ENTRYPOINT ["executable command"]
```

Run the image created by the Dockerfile, binding it to your dev folder:
- `docker run -it -v /path/to/dev/folder/on/host:/path/in/container <node container name or ID> npm init`
- The `-it` flag is needed for the terminal to remain connected to the container so that you can answer the npm project initialization prompts in the terminal.
Example:
- `docker run -it -v /Users/db/docker-projects/node-util/:/app node-util npm init`
- `docker run -it -v /Users/db/docker-projects/node-util/:/app node-util npm install express` --save <-- To install a single package and save it to package.json as a dependency (e.g., express).
- `docker run -it -v /Users/db/docker-projects/node-util/:/app node-util npm install` <-- to install all dependencies from package.json.
*A package.json file will be created on your host machine.*


#### ENTRYPOINT
```Dockerfile
FROM node:14-alpine
WORKDIR /app
ENTRYPOINT ["npm"]
```
No need to prepend 'init' or 'install' with `npm` when using `npm` as the ENTRYPOINT.
- `docker run -it -v /Users/db/docker-projects/node-util/:/app node-util init`

Alternatively to running a `docker run` command, use a docker-compose.yaml file:
```yaml
services:
  npm:
    build: ./
    stdin_open: true
    tty: true
    volumnes:
      - ./:/a
    # entrypoint: ["npm"]
```

The above yaml file will only run the command `npm` after installing node, which is incomplete. 
- `docker-compose up <command>`
- `docker-compose up init` # runs `npm init`

`docker-compose up` is meant to bring up services within a docker-compose.yaml file.

A `run` or `exec` command may be used with docker-compose instead of `up`:
Run a single service by the service name appended to the ENTRYPOINT:
- `docker-compose run <option>`
- `docker-compose run --rm init` # runs `npm init`
- `docker-compose exec init` # runs `npm init`
*Note: `docker-compose run` or `exec` do not remove containers in the same way `docker-compose up` does.*


#### 109. Utility Containers, Permissions & Linux
- https://vsupalov.com/docker-shared-permissions/


## Section 8: A More Complex Setup: A Laravel & PHP Dockerized Project



```yaml
services:
  ...
  php:
    build:
      context: ./dockerfiles
      dockerfile: php.dockerfile
    volumes:
	  # Tell docker to delay updating host machine files to
	  # reflect the corresponding bind mount files.
	  # Files will be updated in batchs rather than
	  # instantly reflecting the changes (as an optimization)
	  # that improved performance.)
      - ./src:/var/www/html:delegated
```

```php.Dockerfile
FROM php:8.2.4-fpm-alpine
WORKDIR /var/www/html
COPY src .
RUN docker-php-ext-install pdo pdo_mysql
RUN addgroup -g 1000 laravel && adduser -G laravel -g laravel -s /bin/sh -D laravel
USER laravel
```


### Bring up specific docker-compose services:
- `docer-compose up -d <service1> <service2>`
- If ervice1 depends on service2, then service2 doesn't need to be added to the up command for both services to start.

### Force Docker to rebuild all layers
- `docer-compose up -d --build <service1>`


## Section 9: Deploying Docker Containers

Google "Docker Hosting Providers"

Largest Providers
- AWS
- Microsoft Azure
- Google Cloud


> [!NOTE]
> #### Important: Installing Docker on a Virtual Machine
> In the next lecture, we'll install Docker on a virtual EC2 instance.
> 
> Please note that the following command (which is used in the next lecture) will unfortunately **not work anymore**:
> ```console
> amazon-linux-extras install docker
> ```
> 
> **Instead, use this approach / these commands:**
> ```console
> sudo yum update -y
> sudo yum -y install docker
> sudo service docker start
> sudo usermod -a -G docker ec2-user
> ```
> 
> Make sure to **log out + back in** after running these commands.
> Once you logged back in, run this command:
> ```console
> sudo systemctl enable docker
> ```
> 
> Thereafter, you can check whether Docker is available by running:
> ```console
> docker version
> ```


 You can follow the Linux setup instructions you find on the official Docker page: [https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/) (under "Server").

