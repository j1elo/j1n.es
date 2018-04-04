---
title: "Today's talk: What's a container?"
date: 2018-04-02T17:08:35+02:00
draft: false

featuredImage: ""
categories: ["talks"]
author: ""

# Set your video id for
youtube: "sK5i-N34im8"
---

There are a lot of misconceptions about what is really a container, such as those managed with Docker. I was in the camp of the people who thought that a container was some kind of "lightweight virtual machine", which could not be further from the truth!

The actual technology that is behind a container engine is _very_ different from a virtual machine: in summary, it's just a `chroot`-ed file system, and the Kernel applying strict policies to access and usage of resources.

<!--more-->
