---
layout: ../../layouts/post.astro
title: '[DevOps Series] Part 3: Docker and the world of containerization'
pubDate: 2025-08-15
description: 'Docker and the world of containerization'
author: 'codingcat'
excerpt: Docker and the world of containerization
image:
  src:
  alt:
tags: ['devops', 'devops-series']
---

# 📚 Series Table of Contents

1. 📖 [Chapter 0: Introduction and Stories](/posts/devops-part0)
2. 📚 [Chapter 1: Some concepts and terminologies](/posts/devops-part1)
3. 🚀 [Chapter 2: A noob guy deploy his web app](/posts/devops-part2)
4. 🐳 [Chapter 3: Docker and the world of containerization](/posts/devops-part3) (You are here) 🎯
5. ☸️ [Chapter 4: K8s in a nutshell](/posts/devops-part4) ⚙️
6. 🔧 [Chapter 5: K8s in details](/posts/devops-part5) 🛠️
7. 🏠 [Chapter 6: Before go to the ground](/posts/devops-part6) 🏡
8. 🐧 [Chapter 7: Ubuntu server and the world of Linux](/posts/devops-part7) 🖥️
9. ⚡ [Chapter 8: MicroK8s the simple and powerful K8s](/posts/devops-part8) ⚙️
10. ☁️ [Chapter 9: Harvester HCI the native cloud](/posts/devops-part9) 🌐
11. 🏭 [Chapter 10: More about Harvester HCI](/posts/devops-part10) 🏢
12. 🖥️ [Chapter 11: Promox VE the best VM manager](/posts/devops-part11) 💾
13. 🌐 [Chapter 12: Turn a server into a router with Pfsense](/posts/devops-part12) 🔌
14. 🛠️ [Chapter 13: Some tools, services that you can installed for your devops pipeline](/posts/devops-part13) 🔧
15. 🌍 [Chapter 14: Hello Internet with Cloudflare Zero Trust](/posts/devops-part14) 🔒
16. 🎉 [Chapter 15: Maybe it the end of the series](/posts/devops-part15) 🏁

---
With me, Docker is something like a "Hello, World" to the Devops world. At first glance, This guy is hard to understand because it comes with a lot of new concepts. In this chapter, I will try my best to simplicify docker for you. So let's start

## Why we need containerization?

This is the reason

![It works on my machine](/devops-series/5.png)

Yes but not everytime Apps work on your machine, it works on mine. Every Applications nowadays have a lot of dependencies, libraries, and other stuff...
![It works on my machine](/devops-series/6.png)

- So think Container is like a bag where you can put in it the OS that you app run, all dependencies, libraries, and other stuff. Then if this bag works on your machine, it will work on every machine. That how Container works and why we need it. Docker is just a implementation of Containerization we have another tool like PodMan, containerd, etc... But docker is the most popular one and easy to use.
- More details how Docker can do it is beyond the scope of this chapter. You can read more or ask AI :D

## Create your first container using Docker

- Enough talking, let's create your first container.
- First, you need to install Docker on your machine. And I recommand you to use Ubuntu to follow most of my blogs. Of course you can use other OS but I will use Ubuntu in this blog. Bye bye Windows user :)) Anyway it just different in install process. Other command and concepts is the same.

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh ./get-docker.sh
sudo docker run hello-world # to test if docker is installed correctly
```

By default, docker deamon will run as root so remember to add `sudo` before every docker command.

- Now let's create a simple container for our nodejs backend. Just let's code a simple nodejs backend.
- Make sure you have nodejs installed.

```bash
mkdir docker-nodejs-backend
cd docker-nodejs-backend
npm init -y
npm install express
```

- Create `index.js` file

```js
const express = require('express');
const app = express();
app.get('/', (req, res) => {
  res.send('Hello World');
});
app.listen(3000, () => {
  console.log('Server is running on port 3000');
});
```

- Run `node index.js` to test if it works.
- Every docker container need a Dockerfile as the Blueprint to build it. You can imagine here is where you can define which items you push in your magic bag.
- Create a file named `Dockerfile` in the root of your project with below content. Read my comment in the file to understand what it does.

```dockerfile
FROM node:20-alpine # This is the base image usually the OS that your app run on here is an alpine linux with node 20 installed 
WORKDIR /app # This is the working directory in the container like mkdir -p /app && cd /app
COPY package.json . # Copy the package.json file to the container
COPY index.js . # Copy the index.js file to the container
RUN npm install # Install the dependencies
EXPOSE 3000 # Expose the port 3000 to the outside world - this line is optional but good to have
CMD ["node", "index.js"] # This is the command to run your app
```

- You can think container is like a VM run in your machine every line in docker file is some commmand that you can run in your VM. How you build and run your local app just bring it to the container. So linux knowledge is very important to understand docker.
- Now let's build the container.

```bash
sudo docker build -t docker-nodejs-backend .
```

- the `-t` is the tag of the container. You can think it as the name of the container. and the `.` is the context of the build. Dot mean find me the Dockerfile in the current directory.
- Now let's run the container.

```bash
sudo docker run -p 3000:3000 docker-nodejs-backend
```

- Now you can access your app at `http://localhost:3000`
- You can see the container is running and the app is running.

LOL just it, Now you can fill in your CV mastered in Docker. :))))

***my confession: I now alway ask AI to write Dockerfile for me. :))))***

## Some basic concepts you must know

- Docker daemon
- Docker image
- Docker registry
- Docker file structure

## Push to Container Registry

## Docker command cheat sheet

## Docker compose for an easier life

## Some advanced concepts

- Layer caching
- Docker network
- Docker engine
- Multi stage build to optimize your image size

---

## 📚 Series Navigation

| **[← Previous Chapter](/posts/devops-part2)**<br>**🚀 A noob guy deploy his web app** | **DevOps Series**<br>**Chapter 3 of 16** | **[Next Chapter →](/posts/devops-part4)**<br>**☸️ K8s in a nutshell** |
