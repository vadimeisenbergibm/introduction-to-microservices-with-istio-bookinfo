# Introduction to microservices with Bookinfo sample application, Kubernetes and Istio
Step-by-step introductory tutorial to microservices based on the [Istio Bookinfo sample](https://istio.io/docs/guides/bookinfo.html).


This tutorial demonstrates a single microservice as a web app, node.js, Docker. Then it proceeds to a whole application (Bookinfo), composed of multiple microservices, managed by Kubernetes with Istio. The learning modules show evolution of the application: development of a single microservice, creating a container, deploying the application to Kubernetes, adding Istio to the Kubernetes cluster, deploying new microservice versions, routing traffic to a new version, and finally, monitoring, logging, distributed tracing, fault injection and security policies. The Istio features are presented as part of the developing story. The focus is on why the presented Istio features are required and what can be achieved using Istio. While presenting Istio features, various microservices concepts are briefly described. In the summary module, links to further Istio documents are provided.

The tutorial supports running commands in multiple namespaces by multiple participants simultaneously. To set up
multiple namespaces, create a namespace per participant, and for each participant set the value of the namespace in the
context of a [kubeconfig](https://kubernetes.io/docs/concepts/configuration/organize-cluster-access-kubeconfig/#the-kubeconfig-environment-variable)
file.

To view the default namespace of a participant run:

```
kubectl config view -o jsonpath={.contexts..namespace}
```

The ideas and scenarios taken from the [Production-Ready Microservices](http://shop.oreilly.com/product/0636920053675.do) book of Susan Fowler and from the [istio.io guides, tasks and blog](https://istio.io).

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
