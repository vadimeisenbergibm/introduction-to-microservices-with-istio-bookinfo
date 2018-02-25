# Tutorial summary
As we saw in the learning modules, Istio provides the following features:
* Control the traffic between the microservices. With Istio you can implement canary deployments, traffic shadowing, phased rollouts and A/B testing.
* Reporting and Monitoring. With Istio you can collect the logs about the traffic between all the microservices, collect metrics, implement a dashboard and calculate the service graph.
* Enforce security policies.
* Implement fault injection.

# Next steps to learn Istio
In addition, Istio can [encrypt the traffic between microservices](https://istio.io/docs/tasks/security/mutual-tls.html). Also, Istio supports various microservices patterns, for example timeouts[https://istio.io/docs/tasks/traffic-management/request-timeouts.html], retries, [circuit breakers](https://istio.io/docs/tasks/traffic-management/circuit-breaking.html).

Also note that Istio can run on VMs, and with service registries other than Kubernetes. Istio can control the traffic from the outside into the service mesh and the traffic to the external services.

See more guides, tasks and blogs at [istio.io](https://istio.ios).
