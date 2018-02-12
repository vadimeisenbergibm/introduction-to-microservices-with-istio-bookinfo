# Logs with Istio
Logs and monitoring are a very important aspect of microservices architecture. It is so important that it is considered one of the three prerequisites for transition to the microservices architecture style. No monitoring - no transition.

In this learning module, we will add collecting logs to our application.

1. We will deploy [Prometheus time series database and monitoring system](https://prometheus.io) for logs collection.
  ```bash
  kubectl apply -f ../../istio-*/install/kubernetes/addons/prometheus.yaml
  ```

2. Define a log stream and a metric for Istio to collect into the Prometheus instance:
  ```bash
  istioctl create -f telemetry.yaml
  ```
  The metric's name is `istio_bookinfo_request_count`.

3. Perform port forwarding from the Prometheus instance to our machine.
  ```bash
  kubectl -n istio-system port-forward $(kubectl -n istio-system get pod -l app=prometheus -o jsonpath='{.items[0].metadata.name}') 9090:9090 &
  ```

4. Access [the Prometheus instance on our localhost](http://localhost:9090/graph#%5B%7B%22range_input%22%3A%221h%22%2C%22expr%22%3A%22istio_bookinfo_request_count%22%2C%22tab%22%3A1%7D%5D) to see our metric values.

5. Swiftch to the Graph tab to see a graph of our metric.

6. See the collected log:
  ```bash
  kubectl -n istio-system logs $(kubectl -n istio-system get pods -l istio=mixer -o jsonpath='{.items[0].metadata.name}') mixer | grep \"instance\":\"newlog.logentry.istio-system\"
  ```

  Note that the log entries from all the bookinfo microservices appear in one place. We do not have to go after each and every microservice and to display their logs one by one.
