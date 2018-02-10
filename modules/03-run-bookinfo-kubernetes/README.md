# Deploy Bookinfo in Kubernetes

1. Deploy to Kubernetes. Notice the scalability - 3 replicas of each service.
  ```
  kubectl apply -f bookinfo.yaml
  ```

1. Edit `ingress.yaml` - specify your host instead of `your host`. For Bluemix, get your host by running: `bx cs clusters`, `bx cs cluster-get <your cluster>`

1. Deploy your ingress
   ```
   kubectl apply -f ingress.yaml
   ```

1. Access http://<your host>/productpage
