# pull-request
Pull an image or a repository from a registry

Syntax:
````
docker pull [OPTIONS] NAME[:TAG]
````
## Example

Code:
````
docker pull centos
````
Output:
![pull centos](https://user-images.githubusercontent.com/79436509/114931514-f718bd80-9e53-11eb-8035-092055b88862.JPG)




# push-request

Docker Push is a command that is used to push or share a local Docker image or a repository to a central repository; it might be a public registry like https://hub.docker.com or a private registry or a self-hosted registry. We need to login to the registry before pushing the Docker image to the registry if proper authentication is setup. Data pushed to the registry is compressed before sending it to the registry.

Syntax:
````
docker push [OPTIONS] NAME[:TAG]
````

[OPTIONS] – We have only one option ‘–disable-content-trust’ in Docker commands and by default it is true.

NAME[:TAG] – We need to specify the name of the registry followed by repository and then the tag of the Docker image.

As we know, we can share images to the public registry or private registry. When we push any image, Docker daemon first checks its tag, how the image is tagged to determine where to push the image. If there is no repository mentioned in the name of the Docker image, it will send it to the [docker.io/library] which requires authentication. Mostly official images are available at that location. So we cannot push any Docker images over there which means we need to re-tag our image before pushing it to the registry. If we have an account on hub.docker.com then we get a default repository with our Docker Id so that we can push our Docker image on hub.docker.com and make it public or keep it private as our requirement.

## Example 1
In the first scenario, we will push the image to the public registry. If we do not re-tag the Docker image, it will push to a public repository [docker.io/library/nginx] however it will require Docker login.

Code:
````
docker login
docker push python_demo
````
Output:
![docker-push denied](https://user-images.githubusercontent.com/79436509/114928958-d69b3400-9e50-11eb-9293-c227e140a576.JPG)

Explanation: In the above example, after providing credentials, tried to push the image to the public registry, however authentication failed as we are pushing it to a public registry. We need to tag the image to send it to our own repository that is created when we sign up on hub.docker.com. It creates a default repository with our Docker ID.

Let’s re-tag the Docker image and try to re-push it to the hub.docker.com once again.

Re-tagged python_demo image with my repository as below: –

Code:
````
docker login
docker tag python_demo neerajshukla165/python_demo
docker push neerajshukla165/python_demo
````

Output:
![docker-push](https://user-images.githubusercontent.com/79436509/114929233-28dc5500-9e51-11eb-82fe-c31308a92f02.JPG)


Explanation: In the above example, we can see that the Docker image is successfully pushed to the hub.docker. com and we can confirm it by logging to hub.docker.com. There should be a new repository created with python_demo and it has a Docker image with the latest tag as if we don’t provide the tag it adds the ‘latest’ tag.

![docker_hub push](https://user-images.githubusercontent.com/79436509/114929599-a1dbac80-9e51-11eb-8c7b-d9e0c409145c.JPG)



## Example 2


Code:
````
docker login
docker tag nginx neerajshukla/nginx
docker push neerajshukla165/nginx
````

Output:
![docker-nginx push](https://user-images.githubusercontent.com/79436509/114930399-963cb580-9e52-11eb-856c-9724759c4bc2.JPG)


In the above example, we can see that the Docker image is successfully pushed to the hub.docker. com and we can confirm it by logging to hub.docker.com. There should be a new repository created with nginx and it has a Docker image with the latest tag

![docker-hub](https://user-images.githubusercontent.com/79436509/114930603-d2701600-9e52-11eb-89e3-f8ebda02e6cf.JPG)

