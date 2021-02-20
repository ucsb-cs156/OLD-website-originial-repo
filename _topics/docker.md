---
topic: "Docker: "
desc: "Virtualization/Container platform"
category_prefix: "Docker: "
---

NOTE: We are NOT CURRENTLY USING DOCKER for W21, but might do so in S21.

# What is Docker?

Docker is a tool for creating/running containers, which are essentially lightweight virtual machines. The main benefit of Docker is that it makes applications much more portable—instead of having to make sure the target machine has exactly the correct dependencies for deployment/local development, you can trust that any machine with Docker installed will be able to run your app.

# Installation

Docker can be installed using [Docker Desktop](https://www.docker.com/products/docker-desktop) on Windows, macOS, and Linux systems. 

# Project Structure

The files required to setup Docker (as implemented in this class), are as follows:
- `Dockerfile` - This is a standard file required by Docker. This file describes how to take a fresh Linux installation and install all of the dependencies required to run your app.
- `dev_environment` - This is a helper script written/maintained by CS156 staff that abstracts away the Docker setup commands from the user. This script builds a "container", or virtualized Linux environment, from the `Dockerfile` and runs a bash shell inside of it.
- `.devcontainer.json` - This is an alternative to the `dev_environment` script for VSCode users. This allows VSCode users to use Docker through the [Remote Development extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack).
