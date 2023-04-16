# Docker 

## Required

- Docker desktop [Download link](https://docs.docker.com/get-docker/)

### or

- Docker ubuntu

Uninstall older versions
` sudo apt-get remove docker docker-engine docker.io containerd runc`

Install last version
`sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`

---

We are going to use Docker to create one container of the APP and another container of the DB, connect between them and save their data using volumes.

**Steps**
- Create image of the APP (Dockerfile)
- Run multi-container (docker-compose.yml) 

## Create image of APP

![Dockerfile](https://github.com/brandonruizmora/docker-node-mongo/blob/master/images/1.png?raw=true)

At first we have to create an image based on the source code. To do this we have to use Dockerfile. Here we define **FROM** where we specify the base image. **RUN** execute linux command to create the folder where the app is going to be stored. **COPY** That is the command to copy the source code and where must be plased. **EXPOSE** The ports that should be exposed. **CMD** Especify the command to run the container.

### Run multi-container

![docker-compose](https://github.com/brandonruizmora/docker-node-mongo/blob/master/images/2.png?raw=true)

Now we have to create the docker-compose.yml file. Where we define the **version**, the **services** (db and app). in **db** we define _the image, container name, port to expose, environment variables, and the volume where the data should be saved._ in **app** we define _the build that says that have to create the image defined in the dockerfile, the container name, the port to expose, the link indicates the name of the container that we want to map that our service app use, depends that specify that this service depend on other container. **volumes** define name of volumen and where to store the data saved.

### Execution

To execute we have to use command _`docker-compose up -d`_

![docker-compose up -d](https://github.com/brandonruizmora/docker-node-mongo/blob/master/images/3.png?raw=true)

Verify the service is running

![localhost:3000](https://github.com/brandonruizmora/docker-node-mongo/blob/master/images/4.png?raw=true)

![docker container logs app](https://github.com/brandonruizmora/docker-node-mongo/blob/master/images/5.png?raw=true)
logs

To end services we use the command _`docker-compose down`_ this command stops the containers and delete them.

![docker container logs app](https://github.com/brandonruizmora/docker-node-mongo/blob/master/images/6.png?raw=true)

---

## Glossary

    Dockerfile

    A Dockerfile is a text-based script that is used to define the configuration and instructions for building a Docker image. Docker is a platform that allows you to create, package, and distribute applications as lightweight and portable containers, which are isolated and contain everything needed to run an application, including the code, runtime, system tools, and dependencies.

    A Dockerfile consists of a series of instructions, which are executed sequentially by Docker to build an image.

    FROM: Specifies the base image to use for building the Docker image. It can be an official Docker image from Docker Hub or a custom image based on another image.

    RUN: Executes commands in the image during the build process. This can be used to install software, configure settings, and perform other tasks required to set up the application.

    COPY or ADD: Copies files from the host machine to the image. This can be used to include application code, configuration files, and other resources in the image.

    WORKDIR: Sets the working directory for subsequent instructions in the Dockerfile. This is where the application code will be placed and where commands will be executed during container runtime.

    EXPOSE: Informs Docker that the container listens on specified network ports at runtime. This does not publish the specified ports to the host machine, but rather documents them for reference.

    CMD or ENTRYPOINT: Specifies the default command to run when a container is launched from the image. This can be an executable, script, or other command that starts the application.

    ENV: Sets environment variables in the image, which can be used to configure the application or set runtime parameters.

    LABEL: Adds metadata to the image, such as version information, maintainer details, and other descriptive information.

    -------------------------------------------------------------

    docker-compose.yml

    docker-compose.yml is a configuration file used by Docker Compose, which is a tool for defining and running multi-container Docker applications. Docker Compose allows you to define a collection of services, each represented by a container, and configure their interactions and dependencies in a single docker-compose.yml file. This makes it easy to manage complex applications with multiple containers.

    The docker-compose.yml file is written in YAML (YAML Ain't Markup Language) format and consists of key-value pairs that define the services, networks, volumes, and other configurations for your Docker application. Here are some common sections in a docker-compose.yml file:

    services: Defines the different services or containers that make up the application. Each service is specified with a name, and its configuration can include the Docker image to use, environment variables, ports to expose, volumes to mount, and other settings.

    networks: Specifies the networks that the services should be connected to. This can include default networks provided by Docker, as well as custom networks defined in the docker-compose.yml file. Networking allows containers to communicate with each other.

    volumes: Defines the volumes that should be created or mounted in the containers. Volumes are used for persisting data generated by the application or for sharing data between containers.

    environment: Sets environment variables that can be passed to the containers. These can be used to configure the application at runtime or provide sensitive information such as passwords or API keys.

    ports: Maps host machine ports to container ports, allowing the containers to listen on specified ports on the host machine for incoming connections.

    depends_on: Specifies the order in which the services should be started. This allows you to define dependencies between services, ensuring that dependent services are started before the services that require them.

    version: Specifies the version of the Docker Compose configuration file format being used. Docker Compose supports different versions with varying features and syntax, and the version is specified at the top of the docker-compose.yml file.


