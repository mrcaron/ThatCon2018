# Devops with Docker

Nick Shultz
NVisia Project Architect

## Intro

DevOps is the combination of pilosophines, practices and tools to increase an organization's ability to deliver at high velocity. This is more about helping people achieve their own ability, not doing it for them. Don't be "The DevOps Team", rather the DevOps coaches.

DevOps is about shrinking the feedback loop, just like Agile. Faster deploys, less failures, reduced cost, collaborate better, etc.

Docker... "Build Ship and Run Any App Anywhere". People tend to start around Dev Environment Tools. 

**Containers** way to package software into standard units for dev, shipment and deployment. It's EVERYTHING bug the kernel that your app needs to run. Services, etc that you'd take time to install. Containers bring Isolation and Security. _Matrix from hell_ slide. Containerize the apps, services, etc and you can deploy it. Spinning up a new staging environment or prod environment... THIS IS INSANE. With Docker, it's defined previously and spun up instantly.

**Vs. VMs**, which are more heavyweight than Containers. You don't need to package up the OS. Containers are smaller, faster to start (minutes -> seconds). VMs are still much more isolated and have dedicated resources. What would happen if you lost a VM? How much headache? For SW... no, we have snapshots that we can spin up instantly. VMs we treat like pets, containers we treat like cattle. We patch VMs all the time. With containers, you don't patch; you release a new container.

_Q: If you can spin up snapshots of a vm easily, does the necessity of a container go away?_

## Example

Angular front end, .NET middle, Java backend. Then he's using VSTS to build and deploy docker containers. Check out docker [UCP](https://docs.docker.com/ee/ucp/ucp-architecture/) (ucp.text.myhost.io). UCP gives a way to interact with the swarm from the machine. It comes with Docker Enterprise Edition. Also that comes with EV is the onprem trusted registry.

> Docker Universal Control Plane (UCP) is the enterprise-grade cluster management solution from Docker. You install it on-premises or in your virtual private cloud, and it helps you manage your Docker cluster and applications through a single interface.

    docker container ls # list containers

If you're using [UCP](https://docs.docker.com/ee/ucp/), you should turn off `docker exec`, it's a security risk. There's no need for it and it increases your potential for security violations. Kuberneties/Docker Swarm is the same kind of stuff, but Kubernetes comes bundled in. DTR = Docker Trusted Reg.

We talk about deploying stacks, described in YAML files (docker compose). Docker Compose is a separate application, running on python, (really nice for local) gives you the option to build it. In the compose file, you specify named services which are individual containers. When you specify named networks, they can address each other by service name. You can specify any number of networks and you need at least one so the services can talk each other, because they behave as individual boxes. Each service is in a directory which contains a dockerfile.

    docker-compose -f <compose yaml file>.yml up     # build and start the images
    docker-compose stop                              # suspends them
    docker-compose down                              # shuts them down, at this time, you can docker up, but no changes 
                                                     #    to the container will be built. you have to remove them first.
    docker rmi $(docker images -f ...)               # removes the docker images you built when you did first compose up

After making any changes to the app, remove the containers completely and rebuild & deploy them. 

DockerFiles can do multi stage builds. Such as

    FROM node:... as builder
    RUN...
    RUN...
    ARG ...

    FROM nginx:...
    RUN...
    COPY --from builder...
    ...

_Not sure I got this, but it's googlable_. _Speaker tip: There was a lot that was glossed over, not really offered as gramatical explaination._

vsts: Docker build agents? The build would normally add the finished docker image to a trusted repo. A _stack file_ is different than _compose_ due to the lack of **build:** directives; otherwise it's the same kind of file. You don't want to use the build directory (compose file) in a production environment. If you want to run a docker service, you want to run a swarm. Then Docker Swarm can handle load balancing?

* [deploy a stack to a swarm](https://docs.docker.com/engine/swarm/stack-deploy/)
* [what's a stack?](https://docs.docker.com/get-started/part5/)
* [Stack files for your service](https://docs.docker.com/docker-cloud/getting-started/deploy-app/11_service_stacks/)
