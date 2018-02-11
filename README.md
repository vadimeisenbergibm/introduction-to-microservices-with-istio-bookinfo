# Introduction to microservices with Bookinfo sample application, Kubernetes and Istio
Step-by-step introductory tutorial based on [Istio bookinfo sample](https://istio.io/docs/guides/bookinfo.html).

Demonstrates microservices as web apps, node.js, docker, Kubernetes, Istio. The modules show evolution of the application: development of a single microservice, creating a container, deploying the application to Kubernetes, adding Istio to the Kubernetes clusters, deploying new microservice versions, routing traffic to the new version, and finally, monitoring, logging, distributed tracing, and security policies.

0. Install node.js and npm, docker and get access to a Kubernetes cluster.

1. Download Istio and Bookinfo source
   ```
   make setup
   ```
2. Go over `modules`, by their prefix number.
