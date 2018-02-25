# Introduction to microservices with Bookinfo sample application, Kubernetes and Istio
Step-by-step introductory tutorial to microservices based on the [Istio bookinfo sample](https://istio.io/docs/guides/bookinfo.html).


Demonstrates microservices as web apps, node.js, docker, Kubernetes, Istio. The modules show evolution of the application: development of a single microservice, creating a container, deploying the application to Kubernetes, adding Istio to the Kubernetes clusters, deploying new microservice versions, routing traffic to the new version, and finally, monitoring, logging, distributed tracing, and security policies.

The ideas and scenarios taken from the [Production-Ready Microservices](http://shop.oreilly.com/product/0636920053675.do) book of Susan Fowler and from [istio.io guides and tasks](https://istio.io).

1. Make yourself familiar with the microservices concept. [The article of James Lewis and Martin Fowler](https://martinfowler.com/articles/microservices.html) is a good place to start.

1. Install [node.js](https://nodejs.org/en/download/), [docker](https://docs.docker.com/install/) and get access to a [Kubernetes](https://kubernetes.io) cluster. For example, you can try the [IBM Cloud Container Service](https://console.bluemix.net/docs/containers/container_index.html#container_index).

1. Download Istio and Bookinfo source:
   ```bash
   make setup
   ```
1. Alias `istioctl`:
   ```bash
   alias istioctl=$(pwd)/istio-*/bin/istioctl
   ```
2. Go over `modules`, by their prefix number, issuing `cd` to each modules's directory.
