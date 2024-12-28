# Pterodactyl Development Environment
This repository provides a `docker-compose` based environment for handling local development of Pterodactyl.

**This is not meant for production use! This is a local development environment only.**

### Getting Started
You'll need the following things installed on your machine.

* [Docker](https://docker.io)
* [Docker Compose](https://docs.docker.com/compose/)
* [mkcert](https://github.com/FiloSottile/mkcert)

### Setup
To begin clone this repository to your system, and then run `./setup.sh` which will configure the
additional git repositories, and setup your local certificates and host file routing.

```sh
git clone https://github.com/pterodactyl/development.git
cd development
./setup.sh
```

#### What is Created
* Traefik Container
* Panel & 2x Wings Containers
* MySQL & Redis Containers

### Accessing the Environment
Once you've setup the environment, simply run `./beak up -d` to start the environment. This simply aliases
some common Docker compose commands.

Once the environment is running, `./beak app` and `./beak wings` will allow SSH access to the Panel and
Wings environments respectively. Your Panel is accessible at `https://pterodactyl.test`. You'll need to
run through the normal setup process for the Panel if you do not have a database and environment setup
already. This can be done by SSH'ing into the Panel environment and running `setup-pterodactyl`.

The code for the setup can be found in `build/panel/setup-pterodactyl`.
All other `docker compose` commands can be used as normal.
