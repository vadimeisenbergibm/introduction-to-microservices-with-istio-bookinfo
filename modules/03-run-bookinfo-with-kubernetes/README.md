# Deploy Bookinfo application that uses _ratings_ microservice in Kubernetes

This learning module shows you an application of four microservices: _productpage_, _details_, _ratings_ and _reviews_. The application is called Bookinfo and is described [here](https://istio.io/docs/guides/bookinfo.html). Consider the application there as the final version, in which the _reviews_ microservice has three versions _v1_, _v2, _v3_. In this module we start with the application with the first version of the _reviews_ microservice, _v1_. In the next modules, we will evolve the application.

1. Skim `bookinfo.yaml` - this is a Kubernetes deployment spec of the app. Notice the services and the deployments, and also the replication: 3 replicas of each microservice.

1. Deploy to Kubernetes.
   ```
   kubectl apply -f bookinfo.yaml
   ```
1. Check the pods status. Notice that each microservice has three pods.
   ```
   kubectl get pods
   ```

1.  Deploy your ingress:

    ```
    MYHOST=$(kubectl config view -o jsonpath={.contexts..namespace}).bookinfo.com kubectl apply -f - <<EOF
    apiVersion: extensions/v1beta1
    kind: Ingress
    metadata:
      name: bookinfo
    spec:
      rules:
      - host: $MYHOST
        http:
          paths:
          - path: /productpage
            backend:
              serviceName: productpage
              servicePort: 9080
          - path: /login
            backend:
              serviceName: productpage
              servicePort: 9080
          - path: /logout
            backend:
              serviceName: productpage
              servicePort: 9080
    EOF
    ```

1. Append the output of the following command to `/etc/hosts`:

   ```
   kubectl get ingress bookinfo -o jsonpath='{..ip} {..host}'
   ```

1. Paste the output of the following command in your browser address bar:

   ```
   kubectl get ingress bookinfo -o jsonpath='http://{..host}/productpage'
   ```

1. Observe how microservices call each other, for example, _reviews_ calls _ratings_ microservice by the URL `http://ratings:9080/ratings`. See the [code of _reviews_](https://github.com/istio/istio/blob/master/samples/bookinfo/src/reviews/reviews-application/src/main/java/application/rest/LibertyRestEndpoint.java):
   ```java
   private final static String ratings_service = "http://ratings:9080/ratings";
   ```
