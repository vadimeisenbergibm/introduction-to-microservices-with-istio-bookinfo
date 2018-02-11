# Deploy Bookinfo application that uses _ratings_ microservice in Kubernetes

This learning module shows you an application of four microservices: _productpage_, _details_, _ratings_ and _reviews_. The application is called Bookinfo and is described [here](https://istio.io/docs/guides/bookinfo.html). Consider the application there as the final version, in which the _reviews_ microservice has three versions _v1_, _v2, _v3_. In this module we start with the application with the first version of the _reviews_ microservice, _v1_. In the next modules, we will evolve the application.

1. Skim `bookinfo.yaml` - this is a Kubernetes deployment spec of the app. Notice the services and the deployments, and also the replication: 3 replicas of each microservice.

1. Deploy to Kubernetes. Notice that each deployment has three pods.
  ```
  kubectl apply -f bookinfo.yaml
  ```

1. Edit `ingress.yaml` - specify your host instead of `your host`.
    * For Bluemix, get your host by running: `bx cs clusters`, `bx cs cluster-get <your cluster>`, `Ingress subdomain` field.

1. Deploy your ingress
   ```
   kubectl apply -f ingress.yaml
   ```

1. Access `http://<your host>/productpage`.

1. Observe how microservices call each other, for example, _reviews_ calls _ratings_ microservice by the URL `http://ratings:9080/ratings`:
   ```bash
   more ../samples/bookinfo/src/reviews/reviews-application/src/main/java/application/rest/LibertyRestEndpoint.java
   ```

   Observe the following line:
   ```java
   private final static String ratings_service = "http://ratings:9080/ratings";
   ```

1. Let's perform some testing of our microservice from inside the cluster. This part exemplifies that you can test your microservices in production! For that, we will use a dummy pod, `sleep`.
   ```
   kubectl apply -f ../../istio-*/samples/sleep/sleep.yaml
   ```

   Once the sleep pod is ready, we can issue HTTP requests from it to our service and test it
   ```
   kubectl exec -it `kubectl get pod -l app=sleep -o jsonpath='{.items[0].metadata.name}'` bash
  curl http://ratings:9080/ratings/7
   ```
1. Let's do some [chaos testing](http://www.boyter.org/2016/07/chaos-testing-engineering/) in production and see how our application reacts. After each chaos operation, access your `http://<your host>/productpage` and see if anything  changed.
   1. Let's kill the _details_ service in one pod.
      ```bash
      kubectl exec -it $(kubectl get pods -l app=details -o jsonpath='{.items[0].metadata.name}') -- pkill ruby
      ```
    2. Let's kill the _details_ services in all its pods.
      ```bash
      for pod in $(kubectl get pods -l app=details -o jsonpath='{.items[*].metadata.name}'); do echo killing  $pod; kubectl exec -it $pod -- pkill ruby; done
      ```
