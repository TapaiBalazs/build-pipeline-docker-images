# build-pipeline-docker-images
This is a repository where I store docker images that are used in build pipelines.

# node-10.16.0-chrome77-openjdk8-CETtime-dind

## Node 10.16.0

This node version is required, because some of our dependencies require it and we didn't have the time to update them.

## Chrome 77

Our Angular projet uses Karma and Jasmine as an unit testing tool and we like to run them in headless chrome.

## Openjdk 8

After we lint and unit test our project we run SonarQube analysis on them and the sonar scanner requires JAVA.

## CET time

We have cypress tests with lots of fixtures. Those fixtures contain timestamps and our tests sometimes assert that the displayed time is the same.
Since the tests were written on a computer which uses CET time the docker container should set it.

## Docker in Docker

Our built application is deployed as an nginx static site, therefore it is imperative that our tests run against our built image running inside a docker container. Since our build runs inside a docker container, Docker in Docker (dind) is necessary for us.
