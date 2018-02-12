# Fault injection with Istio

In this learning module, we inject a fault, error 418 on the path from the _ratings_ microservice to the _reviews_ microservice.

1. Let's add a rule to inject a fault on requests to _reviews_, for our test user `jason`:
  ```bash
  istioctl create -f route-rule-reviews-fault-418.yaml
  ```

1. Let's access the webpage of the application, login as `jason` and see that now an error is displayed instead of the reviews.

1. Also, let's see the error 418 appear in the logs of the sidecar proxy of the `productpage`:

  ```bash
  kubectl logs -l app=productpage -c istio-proxy
  ```
  You should see something similar to:
  ```
  [2018-02-12T14:52:15.126Z] "GET /reviews/0 HTTP/1.1" 418 FI 0 18 0 - "-" "python-requests/2.18.4" "8410206d-d471-9816-9cd5-d3780edc5ab6" "reviews:9080" "-"
  ```
1. Let's logout, login as some other user, and see that other users are not effected by the fault.
