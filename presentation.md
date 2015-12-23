layout: true
background-image: url(images/bg.jpg)
class: center, middle

---

<img class="no-border" src="images/Docker.png">

# The Docker Basics

---

# Agenda

1. What is Docker?
2. Reasons
3. Benefits
4. Installation
5. CLI interface
6. GUI?

???

WAIT
So, let's start. What is Docker?
NEXT

---

# What is Docker?

![Default-aligned image](images/docker-man.min.jpg)

A person employed in a port to load and unload ships

???

WAIT

Do you think I'm joking?

NEXT

---

# Are you kidding me?

![Default-aligned image](images/google-docker-definition.png)

???

WAIT

No, I'm seriously. At the very beginning of google search results
you can see it by yourself. But to be honest...

NEXT

---

# Gotcha!

![Default-aligned image](images/google-docker-first-link.png)

???

Google knows wait I really mean :)

---

# How it works?

![Default-aligned image](images/docker-how-it-works.png)

???

Explanation from official site:

Docker containers wrap up a piece of software in a complete filesystem
that contains everything it needs to run: code, runtime, system tools,
system libraries – anything you can install on a server.

This guarantees that it will always run the same,
regardless of the environment it is running in.

---

# Docker Containers vs Virtual Machine

![Default-aligned image](images/containers-vs-virtual-machines.png)

???

We will use comparison with VM. Who have ever ever used VMs? I mean
VirtualBox, Vagrant, VMWare, etc. etc. Sorry guys who never ever used it.
Maybe some things will be harder to understand.

NOT READ ALL STUFF BELOW IF NOBODY LIKES FIRST DEFINITION!

One more official definition.

### General

Containers have similar resource isolation and allocation benefits
as virtual machines but a different architectural approach allows
them to be much more portable and efficient.

#### Virtual Machines

Each virtual machine includes the application, the necessary binaries
and libraries and an entire guest operating system -
all of which may be tens of GBs in size.

#### Containers

Containers include the application and all of its dependencies,
but share the kernel with other containers. They run as an isolated process
in userspace on the host operating system. They’re also not tied
to any specific infrastructure – Docker containers run on any computer,
on any infrastructure and in any cloud.

---

# Reasons

---

# Docker is Interesting

![Default-aligned image](images/library.jpg)

---

# Everybody Uses It

![Default-aligned image](images/companies.jpg)

---

# Even This Guy

![Default-aligned image](images/homeless.jpg)

---

# Enhance your CV

![Default-aligned image](images/businessman.jpg)

???

It's enhanced version of previous guy. It's AFTER starting
use docker. Previous guy - it BEFORE. ;)

---

# Really?

![Default-aligned image](images/will-stephen.png)

???

If you listen this guy carefully, you understand that
I talk nonsense.("say stupid things"; google, what are you doing with me, haha)

---

<img class="no-border" src="images/TrollFace.png">

???

No one reason above can't be enough for learning smth. new

As for me, I prefer to find major benefits in every thing I found popular.
If I find benefits and they're big enough - only in that case I start
learning that thing. So, benefits.

---

# Benefits

1. Lightweight services
2. Flexible DevOps
3. Reproduce unreproducable

---

# Lightweight services

![Default-aligned image](images/lightweight-services.jpg)

???

### Background story

I had a weak comp before but for now still same habits.

I like when my comp don't load unnecessary things
b/c I can't suppose when exactly I'll need his full power.

I like when I can install some specific software without pain.

---

# Flexible DepOps

![Default-aligned image](images/flexible-devops.jpg)

???

You want to have n different versions of software product
in same moment without pain?(I mean prod, staging, pre-prod) - Docker!

You want to choose one of a few third party service to connect with your? - Docker!

You want to move all stuff you have over here to over there? - Docker!

[Repeat] You want to save some specific OS configuration

---

# Reproduce unreproducible

![Default-aligned image](images/can-not-reproduce.png)

???

When we told about infrastructure based on Docker, we actually talk about
linked between each other containers. They are one piece, which you can easily
give to trusted developers for re-run and reproduce.

---

# Installation

0. Add gpg key
1. Set source list
2. Install

???

Looks simple? Hold on!

---

# Add gpg key

```
# Way 0
wget -qO- https://get.docker.com/gpg | sudo apt-key add -

# Way 1
apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys LOL_KEY
# see actual key on https://docs.docker.com/engine/installation/ubuntulinux/
```

---

# Set source list

```
echo 'deb https://apt.dockerproject.org/repo ubuntu-trusty main' | sudo tee /etc/apt/sources.list.d/docker.list
```

---

# Installation

```
# Way 0
wget -qO- https://get.docker.com/ | sh

# Way 1
sudo apt-get update
sudo apt-get install docker-engine

# Way 2
sudo apt-get install lxc-docker lxc-docker-1.9.1
```
---

![Default-aligned image](images/flow.png)

???

WAIT

Totally: 6 officially described ways... in linux...
More - not described in off docs. And more - with other OSs.

NEXT... why we need to increase complexity so.

---

![Default-aligned image](images/why.jpg)

---

![Default-aligned image](images/shrug.gif)

???

WAIT

I don't know...

You know, when I was preparing, I gonna explain how to install
Docker on Mac and Windows as well. But... When I saw this image
in one of official installation docs, I was feeling bad.

NEXT

---

<img class="no-border" src="images/terminal.png">

???

Explanation of console... No, guys, I can't look there.
Maybe if you don't understard how it works Docker is not for you?
Anyway.

So let's realize we already have installed docker engine.
Let's brief look into cli? Ok, but at first let's have
quick dive in theory.

---

# A Bit of Theory

???

Many people starts here from images or containers.
But I think Layers should be at first

---

# Layer

![Default-aligned image](images/layers.gif)

???

Let's compare it with virtual machine. We have snapshotes there
for keep things in saved state. If you made changes and want
to save it and reuse or just for backup, you do snapshot of
the whole system. Layers work different. It's just diff between
before and after state. Procs and cons:

+ lightweight cause of just diff
- can't be applied only to parrent layer (no cherry-pick here)

Raw layers are no-sense. For make they reusable we must be sure
they in completed state. Images for that.

---

# Image

![Default-aligned image](images/image.jpg)

???

Image - complited bunch of layers, which contain smth. useful inside.
Can be different types: base, like ubuntu:14.04; and specific mquandalle/wekan
Images have id, name and tag(optional). Also every image have specific
start options: exposed ports, workdir, env varialbes, entrypoint.

---

# Examples

## ubuntu:14.04

## mquandalle/wekan

???

We want to use image functionality in some way. Have no sense without containers. 
B/c it's just bunch of layers with ability to configure before start.
For run actually start we need container abstraction.

---

# Container

<img class="no-border" src="images/container.png">

???

Writable/executable layer on top of last image layer. It runs OS
with arguments and configuration of image and create separate
environment from host OS. You can think about it like an instance of class.
Class - image. You can run one or a few of instances of same image.
It'll name 'containers'. For example, you wanna training scaling skill.
You just pull postgre image from Docker Hub and run a few containers of
this image. Link it to master and voila - you have 6 years of experience
in scaling big data projects. Awesome? I think it is.

Any question on this section? Maybe let's briefly disscuss it just now,
before start review actual interfaces?

#### Super optional

Btw, now you should understard why drawing docker as delivery of containers
is stupid. You'll deliver not containers, but IMAGES! Damm marketing.

---

# CLI interface

![Default-aligned image](images/cli.jpg)

---

# Pretty Basics

```
docker ps [-a]
docker images
docker run [options] IMAGE
docker stop CONTAINER
docker start CONTAINER
docker exec [options] CONTAINER
docker logs
docker inspect
docker inspect postgres | grep \"IPAddress\" | head -n 1
docker inspect postgres | grep \"HostPort\" | head -n 1
docker rm CONTAINER
docker rmi IMAGE
```

???

## It would be nice if you'll have enough time to show demo here

I'm sure you will not use port forwarding to reduce pain. You'll try
to keep best practices. So you'll find botton spagetti command very useful.
Especially when you'll need to check if recently runned service works.

---

# Also

- Dockerfile
- Build, autobuild
- Docker Hub. What is it and why I should care?
- Tagging, push, pull
- etc. etc.

---

# GUI

- https://www.docker.com/docker-toolbox
- https://docs.docker.com/mac/started/
- https://docs.docker.com/windows/started/

---

# Brief Recap

- You don't have to learn smth. new just because 
- Docker is useful for
  * services
  * DevOps
  * bugfixing
- Only 10 main command line commands

---

# The End

---

# Questions?

???

No question anymore? So, I have one for you: where I'm lied in this talk?
