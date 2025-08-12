---
layout: ../../layouts/post.astro
title: '[DevOps Series] Part 1: Some concepts and terminologies'
pubDate: 2025-08-08
description: 'Just an overview of some concepts and terminologies in DevOps that I think you should know'
author: 'codingcat'
excerpt: Just an overview of some concepts and terminologies in DevOps that I think you should know
image:
  src:
  alt:
tags: ['devops', 'devops-series']
---

# 📚 Series Table of Contents

1.  📖 [Chapter 0: Introduction and Stories](./devops-part0)
2.  📚 [Chapter 1: Some concepts and terminologies](./devops-part1) (You are here) 🎯
3.  🚀 [Chapter 2: A noob guy deploy his web app](./devops-part2) 💻
4.  🐳 [Chapter 3: Docker and the world of containerization](./devops-part3) 📦
5.  ☸️ [Chapter 4: K8s in a nutshell](./devops-part4) ⚙️
6.  🔧 [Chapter 5: K8s in details](./devops-part5) 🛠️
7.  🏠 [Chapter 6: Before go to the ground](./devops-part6) 🏡
8.  🐧 [Chapter 7: Ubuntu server and the world of Linux](./devops-part7) 🖥️
9.  ⚡ [Chapter 8: MicroK8s the simple and powerful K8s](./devops-part8) ⚙️
10. ☁️ [Chapter 9: Harvester HCI the native cloud](./devops-part9) 🌐
11. 🏭 [Chapter 10: More about Harvester HCI](./devops-part10) 🏢
12. 🖥️ [Chapter 11: Promox VE the best VM manager](./devops-part11) 💾
13. 🌐 [Chapter 12: Turn a server into a router with Pfsense](./devops-part12) 🔌
14. 🛠️ [Chapter 13: Some tools, services that you can installed for your devops pipeline](./devops-part13) 🔧
15. 🌍 [Chapter 14: Hello Internet with Cloudflare Zero Trust](./devops-part14) 🔒
16. 🎉 [Chapter 15: Maybe it the end of the series](./devops-part15) 🏁

---

Anyone who starts learning DevOps may think, "What the f\*ck is all this stuff for? I just want to deploy my app." Yes, starting with a simple Node.js backend is easy, but then you need to deal with Virtual Machines, Containers, Kubernetes, CI/CD, Nginx, IP addresses, domains, DNS, etc. I've been there too, so in this series, I'll provide an overview of all these terminologies and concepts that we'll discuss in later chapters.

### 1. What is DevOps?

DevOps is a set of practices and tools that help organizations deliver software faster and more efficiently. It combines development (Dev) and operations (Ops) to create a seamless workflow that allows for continuous delivery and deployment.

### 2. Difference between Cloud services and self-hosted (ground)

Cloud services are provided by third-party providers like AWS, GCP, Azure, etc. You pay for what you use, and you don't need to worry about the underlying infrastructure. For self-hosted solutions, you need to manage the infrastructure yourself, install the OS on your server, install the software, configure the network, etc.

### 3. Virtual Machines

Just like a real machine but running inside another machine. Some VM software like VirtualBox, VMware, etc. can help you create a virtual machine. Virtual machines run on your computer but with separate OS, network, etc. Cloud service providers like AWS, GCP, Azure, etc. also provide virtual machines.

### 4. Stories about IP address

- Any device that connects to the internet has an IP address, even Virtual Machines. Usually, we should have a public IP address for devices that connect to the internet. But the amount of IPv4 addresses is not enough for all devices, so now Internet Service Providers (ISPs) use a technique called NAT (Network Address Translation) to share the same IP address among many devices in a Local Area Network (LAN). So usually, we have a private IP address for devices in the LAN, which looks like 192.168.1.100. This is important because, unlike when we use cloud service providers who always have a public IP address for services that we use, for self-hosted solutions we need to use private IP addresses (LAN IP addresses).
- Now to solve the IPv4 shortage problem, IPv6 comes to the rescue. IPv6 is a 128-bit address that can be used to identify any device on the internet. But it's not easy to remember and type, so we use domain names to identify devices. Also, not all devices support IPv6, so we need to use IPv4.
- Fun fact: AWS Lightsail now charges you money for each public IP address, and in a data center, you need to buy public IPv4 addresses if you want to get a public IP for your server.
- But in this series, you will learn how to let anyone access your services without any public IP, just using private LAN IPs.

### 5. Why we need containers?

You can just create a VM, install the environment, and run your app in it. But it's not efficient because you need to install the same environment for each VM. So we need a way to package the environment and the app into a container.

### 6. Why K8s?

When a single container is not enough to handle all requests, we scale it up, but when scaling multiple containers, it's hard to manage all of them. Then we use Kubernetes, which is a container orchestration platform that allows you to manage containers across multiple nodes (a node is just a computer for easier understanding).

### Still a lot of another things too

As you see in the world of DevOps, people create a tool to solve a problem, but the funny thing is that the tool creates another problem. So they will create another tool to solve the problem created by the first tool. :))) In this series, you will see this endless loop :v In this blog, I just show an overview of some terms that we talk about a lot in this series.

You don't need to understand all of these now. Let's just go to the next step of our journey: [Chapter 2: A noob guy deploy his web app](./devops-part2) 💻

---

## 📚 Series Navigation

| Previous Chapter                                                            |               Series Info                |                                                                 Next Chapter |
| :-------------------------------------------------------------------------- | :--------------------------------------: | ---------------------------------------------------------------------------: |
| **[← Previous Chapter](./devops-part0)**<br>**📖 Introduction and Stories** | **DevOps Series**<br>**Chapter 1 of 16** | **[Next Chapter →](./devops-part2)**<br>**🚀 A noob guy deploy his web app** |
