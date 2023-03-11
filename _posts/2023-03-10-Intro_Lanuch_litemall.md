---
layout: post
title: "Intro of litemall and Lanuch"
date:   2023-03-08
tags: [litemall]
comments: true
author: GingerNg
---

## Intro
[Litemall](https://github.com/liutaojava/litemall) was developed  by [liutaojava](https://github.com/liutaojava) 3 years ago. It is a project built on vue, java, springboot and mysql. Recently, I have some interest in Java development, so I decide to delve into it. I have forked the [repo](https://github.com/GingerNg/litemall) with some modification.

As the architecture shows that, from technology, it consists of frontend, backend and db. From business, it have mall and admin systems. We will introduce how to launch admin system below.
![arch of litemall](https://s2.loli.net/2023/03/11/6yJZK4DwoIgchUG.png)
## Lanuch
First of all, we need to install mysqldb and initial db using the provided [sql files](https://github.com/GingerNg/litemall/tree/master/litemall-db/sql)


#### Backend
Firstly, jdk-11 and maven are required to install. Then use **mvn clean package**, maven will download the dependencies of litemall. A file named as itemall-admin-api-0.1.0-exec.jar will appear the **target** fold.
Before launching, configure the IP and port of db for Backend. At last, use **java -jar itemall-admin-api-0.1.0-exec.jar** to launch the server.

#### Frontend
**nvm**(Node Version Management) is a useful tool to intall node.js. **v14.0.0** is a validated version for litemall-admin.
Use __nvm install v14.0.0__, and the corresponding version of npm will installed too.
Then, use __npm i__ to install the dependencies.
Before launching, configure the backend url for Frontend
Finally, __npm run dev__.

After all the opeartion above, Open your browser and enter the url of Frontend, you will see the login and dashboard page,

![login page](https://s2.loli.net/2023/03/11/fhQeHwnx5dSG3vy.png)

![dashboard page](https://s2.loli.net/2023/03/11/XEzsQFtvua6mRB7.png)

