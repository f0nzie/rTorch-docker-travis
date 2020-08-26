These are some instructions to build and run a Travis machine locally.
We attempt to run all the tests usually run at http://travis-ci.org in a Docker container maintaining the same characteristics of a Travis remote machine.



## Motivation

The goal is reducing the time that takes debugging an error in Anaconda environments when installing PyTorch or rTorch. The bugs remain hidden in the local development machine and only pop up in a Travis machine. That prevent us to complete the tests as the Travis tests can never be completed. There is always doubts of what bug is causing the problem.



## Build Docker image

```
docker build -t my-travis .
```


## Run container with travis

```
docker run --rm --name my-travis-kont -dit my-travis /sbin/init
docker exec -it my-travis-kont bash -l
```