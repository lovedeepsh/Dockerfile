# Kube-state-metrics

This is a repo for Kube-Metrics-Deployement with customized docker image.

## To build Image from [Master](https://github.com/abhishekbhardwaj510/kube-state-metrics/)

In this branch image will be build from scratch and will use binary executable file with port no. *8080*.
```
docker build -t {{image_name}}:{{tag}} Dockerfile . 
```
There is another branch [Release-1.0](https://github.com/abhishekbhardwaj510/kube-state-metrics/tree/Release-1.0) which contains the [Dockerfile](https://github.com/abhishekbhardwaj510/kube-state-metrics/blob/Release-1.0/DockerFile) with [Go](https://golang.org/) langauge to setup environment for kubernetes cluster and pod monitoring with prometheus.

**Default port no. for Kube-state-metrics is 8080**

## To build Image in [Release-1.0](https://github.com/abhishekbhardwaj510/kube-state-metrics/tree/Release-1.0)

In this branch image will build by from **golang** and after that *make* command will create a binary executable file with default port no. *8080*
```
docker build -t {{image_name}}:{{tag}} Dockerfile .
```


