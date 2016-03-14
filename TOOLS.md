# **HOWTO Guide for Docker and [Vagrant](https://www.vagrantup.com)**

## **Overview**

[Docker](https://www.docker.com/) is a tool system for automating containers, a way to segregate application environments.  [Vagrant](https://www.vagrantup.com) is a tool for automating virtual machines through the command line.  [Vagrant](https://www.vagrantup.com) has a provisioning system, which can use shell scripts, robust change configuration systems, or [Docker](https://www.docker.com/).

As [Docker](https://www.docker.com/) only runs on Linux, [Windows](https://www.microsoft.com/en-us/windows) or [Mac OS X](http://www.apple.com/osx/) users will need to use a virtual machine like Virtualbox to run containers.  [Docker Machine](https://docs.docker.com/machine/) can create such an environment where a [Docker](https://www.docker.com/) tool maps to a [Linux](http://www.linuxfoundation.org/) system running on Virtualbox.  This environment is a minimalist system (uses [Boot2Docker](http://boot2docker.io/)'s image based on [Tiny Core Linux](http://tinycorelinux.net/)) used only for running containers.

For a more robust environment, you can use [Vagrant](https://www.vagrantup.com) to build [Docker](https://www.docker.com/) images and run containers.

## **Getting the Tools**

You can get [Docker](https://www.docker.com/) and [Vagrant](https://www.vagrantup.com) from these sites below:

* Windows or Mac OS X:
   * [Virtualbox](https://www.virtualbox.org/wiki/Downloads) - https://www.virtualbox.org/wiki/Downloads
   * [Docker Toolbox](https://www.docker.com/products/docker-toolbox) ( [Windows](https://www.microsoft.com/en-us/windows) or [Mac OS X](http://www.apple.com/osx/) only) - https://www.docker.com/products/docker-toolbox
   * [Vagrant](https://www.vagrantup.com/) ([Windows](https://www.microsoft.com/en-us/windows), [Mac OS X](http://www.apple.com/osx/), [Debian](https://www.debian.org/), or [CentOS](https://www.centos.org/)) - https://www.vagrantup.com/
* Linux:
   * *Install from Internet*: `curl -fsSL https://get.docker.com/ | sh`
   * *Install from Repository*: https://docs.docker.com/engine/installation/

### **Windows**

Alternatively, you can use [Chocolately](https://chocolatey.org/) to install some of these tools:

```batch
:: Virtualbox Components
choco install virtualbox
choco install virtualbox.extensionpack
:: Docker Components
choco install docker
choco install docker-machine
choco install docker-compose
:: Vagrant Components
choco install vagrant
```

### **Mac OS X**

[Cask](https://caskroom.github.io/):
```bash
# Virtualbox Components
brew cask install virtualbox
brew cask install virtualbox-extension-pack
# Vagrant
brew cask install vagrant
# Docker Toolbox
brew cask install dockertoolbox
```

## **Basic Vagrant**

[Vagrant](https://www.vagrantup.com/) can be complex to use:

```bash
$ vagrant up
```

## **Basic Docker**

### **Docker Machine**
As [Docker](https://www.docker.com/) requires Linux containers, you need to Linux system to use [Docker](https://www.docker.com/).  For this you can use [Docker Machine](https://docs.docker.com/machine/).

```bash
docker-machine create -d virtualbox toolbox
eval "$(docker-machine env toolbox)"
```

### **Docker Workflow**

The basic docker workflow for these projects are:

```bash
docker build -t mywebapp .
docker run -p 8080:8080 -d mywebapp
```

### **Docker Compose**

If a `docker-compose.yml` file is provided, you can use [Docker Compose](https://www.docker.com/products/docker-compose).  This used to be called [Fig](http://www.fig.sh/).

```bash
docker-compose up -d
```

## **Testing Results**

The ports may vary depending on project.

```bash
$ [ -z ${DOCKER_MACHINE_NAME} ] || WEBSERVER=$(docker-machine ip ${DOCKER_MACHINE_NAME})
$ WEBSERVER=${WEBSERVER:-localhost}
$ PORT=8080
$ curl -i http://${WEBSERVER}:${PORT}
Hello World!
$ curl -i http://${WEBSERVER}:${PORT}/hello/Yehoyaqim
Why Hello Yehoyaqim!
```