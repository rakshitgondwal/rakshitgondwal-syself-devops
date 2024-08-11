## What were the decisions I made while writting this Helm chart?

This Helm Chart deploys a sample go backend application to a Kubernetes cluster. I'll further explain the decisions and best practices I've while writing this chart.

What all things I did to make it production ready?

* The image that is being pulled in the Deployment template from `values.yaml` has a specific tag defined. This is because, having latest as the image tag is not always a best practice and can often raise concerns in a security angle and sometimes we might want to use this chart for different versions in different environments.

* All the resources are namespaced. This will keep the resources isolated and avoids conflicts with other applications running in different namespaces.

* Defined resource requests and limits in the deployment template.This helps to avoid resource contention and ensures that the application gets the necessary resources without impacting other workloads.

* Included liveness and readiness probes in the deployment template. This will ensure that Kubernetes can detect if the application is healthy and ready to accept traffic.

* Added HPA configuration to automatically scale the number of pods based on CPU and memory utilization.
