# In this module we will add Istio and redeploy our application, Istio enabled.
1. Undeploy our application
   ```bash
   kubectl delete -f ../03-run-bookinfo-with-kubernetes/bookinfo.yaml
   kubectl delete -f ../03-run-bookinfo-with-kubernetes/ingress.yaml
   kubectl delete -f ../05-adding-a-new-version-of-a-microservice/bookinfo-reviews-v2-with-app-label.yaml
   ```
1. Install Istio
   ```bash
   kubectl apply -f ../../istio-*/install/kubernetes/istio.yaml
   ```
1. Verify that Istio is started correctly, all the pods in `istio-system` namespace are running.
   ```bash
   kubectl get pods -n istio-system
   ```
1. Deploy Bookinfo application, Istio-enabled
   ```bash
   kubectl apply -f <(istioctl kube-inject -f ../03-run-bookinfo-with-kubernetes/bookinfo.yaml)
   ```
1. Deploy Istio-enabled ingress. Note that it is written slightly differently than the ingress we used for Kubernetes without Istio. Istio-enabled ingress has the annotation `kubernetes.io/ingress.class: "istio"`, and it has no host defined. Check [Determining Ingress IP and Port](https://istio.io/docs/guides/bookinfo.html#determining-the-ingress-ip-and-port) for instructions for your cloud.
   ```bash
   kubectl apply -f <(istioctl kube-inject -f ingress.yaml)
   ```

   For _Bluemix Container Service_, use the following:
   1. Get the host IP of the `istio-ingress` pod.
      ```bash
      kubectl get po -l istio=ingress -n istio-system -o 'jsonpath={.items[0].status.hostIP}'
      ```
   2. Get the public IP of the node on which `istio-ingress` runs:
      ```bash
      bx cs workers <your cluster name> | grep <the host IP of istio-ingress>
      ```
   3. Get the port of the `istio-ingress` service:
      ```bash
      kubectl get svc istio-ingress -n istio-system -o 'jsonpath={.spec.ports[0].nodePort}'
      ```
   4. Use the public IP from the step _ii_ and the port from the step _iii_ to access the application. 
   
 1. Access the application after determining Ingress IP and port. Note that Istio was added **transparently**, the original application did not change.
 
 2. Check the application pods and see that now each pod has two containers. The first container is the microservice itself, the second is the sidecar proxy attached to it.
