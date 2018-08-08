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

Angular front end, .NET middle, Java backend. Then he's using VSTS to build and deploy docker containers. Check out docker UCP (ucp.text.myhost.io). UCP gives a way to interact with the swarm from the machine.

    docker container ls # list containers