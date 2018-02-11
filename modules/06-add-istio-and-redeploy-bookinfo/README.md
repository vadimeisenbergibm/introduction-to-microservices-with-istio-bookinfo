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

1. Verify that Istio is installed
  ```bash
  kubectl get pods -n istio-system
  ```
1. Deploy Bookinfo application, Istio-enabled
  ```bash
  kubectl apply -f <(istioctl kube-inject -f ../03-run-bookinfo-with-kubernetes/bookinfo.yaml)
  kubectl apply -f <(istioctl kube-inject -f ../03-run-bookinfo-with-kubernetes/ingress.yaml)
  ```
