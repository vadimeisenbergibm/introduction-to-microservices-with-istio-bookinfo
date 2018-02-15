# Introduction to microservices with Bookinfo sample application, Kubernetes and Istio
Step-by-step introductory tutorial to microservices based on [Istio bookinfo sample](https://istio.io/docs/guides/bookinfo.html).


Demonstrates microservices as web apps, node.js, docker, Kubernetes, Istio. The modules show evolution of the application: development of a single microservice, creating a container, deploying the application to Kubernetes, adding Istio to the Kubernetes clusters, deploying new microservice versions, routing traffic to the new version, and finally, monitoring, logging, distributed tracing, and security policies.

The ideas and scenarios taken from the [Production-Ready Microservices](http://shop.oreilly.com/product/0636920053675.do) book of Susan Fowler.

0. Install node.js and npm, docker and get access to a Kubernetes cluster.

1. Download Istio and Bookinfo source
   ```bash
   make setup
   ```
1. Alias istioctl
   ```bash
   alias istioctl=$(pwd)/istio-*/bin/istioctl
   ```
2. Go over `modules`, by their prefix number, issuing `cd` to each modules's directory.
