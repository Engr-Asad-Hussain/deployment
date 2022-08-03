# Dockerfile
Protected Services (PS) Dockerfile

## Contents
- [A Little Container Knowledge](#a-little-container-knowledge)
- [Layers Concept](#1-layers-concept)
- [Incremental Build](#2-incremental-build)
- [Internal Cache](#3-internal-cache)
- [Effective Steps](#4-effective-steps)
- [References](#5-references)


## A Little Container Knowledge
Everyone of us is interacting with Docker containers and Dockerfile whether he belongs to Software Team as dockerizing frontend or backend services or DevOps Team in creating containers and jenkins servers.

It is important to understand the Docker Concept in order to work more productively and effectively.

### 1. Layers Concept
Each instruction in the Dockerfile creates an image layer. On each line of statement in Dockerfile, it will add a layer. Subsequent layers will be added on top of each other and creates a stack of layers. The more layers it has, the bigger the final image. 

What does it means is? If we have 10 lines of code in Dockerfile, it will end up in creating 10 layers of image.


### 2. Incremental Build
Hence, you should minimize the number of RUN commands and stack all of them as one whenever possible. For example, instead of having two different RUN commands in your DockerFile, as shown below:

```RUN python -m pip install -U pip```

```RUN pip install -r requirements.txt```

You should combine them into one as follows:

```RUN python -m pip install -U pip && pip install -r requirements.txt```


### 3. Internal Cache
Docker has its own internal cache which will reuse the same layer if a file did not change since the last build. Since requirement files and the installation does not change frequently, you can write your DockerFile in this way to reuse the same layers each time you rebuild the container image.


### 4. Effective Steps
Each instruction in the Dockerfile creates an image layer, and the upper layer depends on the lower layer. At any time, as long as a layer changes, the caches of all layers above it will be expired.
In other words, if we change the execution order of Dockerfile instructions, or modify or add instructions, the cache will expire.
```
FROM python:3.10
WORKDIR /app
COPY ./app .
RUN pip install -r requirements.txt
ENTRYPOINT [ "python" ]
CMD [ "/app/app.py" ]
```
So, write Dockerfile in such a way you can take advantage of the cache concept of docker. For example, we know mostly requirements.txt wouldn't change frequently as the code inside 'app' folder does. So why not to follow the standards and create a docker file as follows:
```
FROM python:3.10
WORKDIR /app
COPY ./app/requirements.txt .
RUN pip install -r requirements.txt
COPY ./app .
ENTRYPOINT [ "python" ]
CMD [ "/app/app.py" ]
```
Now, it will cache the requirements.txt step and you would end up in much faster build time as before.


### 5. References
[1] https://betterprogramming.pub/6-concepts-to-master-when-dockerizing-python-applications-e5f5a6a87845

[2] https://blog.devgenius.io/container-image-caching-d2c49f5343a4
 
