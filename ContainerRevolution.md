# Container Revolution
@jbogard; jimmy bogard
... Walked in Mid Conf

Talking about Docker Compose; easy to setup development environment. Dev environment can be containerized and started up when developing and running integration testing. 

## Decisions

What things should be in docker vs. what about outside of docker?

Think of docker images as well isolated processes; services. 

Create a container to do the build in, spin it up, build it and if it works, you can avoid the "builds on my machine" syndrome. Like CI, but flexible.

AppVeyor is popular

Docker for builds can be data and time expensive. To do this efficiently, this would need persistent agents. Host it yourself, via Kubernetes, or whatever.