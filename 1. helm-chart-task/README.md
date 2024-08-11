## What were the decisions I made while writting this Helm chart?

This Helm Chart deploys a sample go backend application to a Kubernetes cluster. I'll further explain the decisions and best practices I've while writing this chart.

* The image that is being pulled in the Deployment template from `values.yaml` has a specific tag defined. This is because, having latest as the image tag is not always a best practice and can often raise concerns in a security angle and sometimes we might want to use this chart for different versions in different environments.

* A Production grade helm chart usually has dependency to other charts, which are explicitly mentioned in the `Chart.yaml`, but since this is a sample application :) I couldn't implement a dependency for this chart, but usually there is an another `charts/` dir and a `Charts.lock` file to lock the dependencies.

* I modified the `Chart.yaml` to have some extra fields such as `keywords` and `sources`. I don't think these make a chart more of a production ready but it makes it looks good so why not.

* All the resources are namespaced. This will keep the resources isolated and avoids conflicts with other applications running in different namespaces.

* Defined resource requests and limits in the deployment template.This helps to avoid resource contention and ensures that the application gets the necessary resources without impacting other workloads.

* Included liveness and readiness probes in the deployment template. This will ensure that Kubernetes can detect if the application is healthy and ready to accept traffic.

* Added HPA configuration to automatically scale the number of pods based on CPU and memory utilization.

## What Database would I choose for this application?

Before choosing a db for my application, I would take these things into consideration:
* Do I really need a heavyweight DB for this application?
* How simple will it be to set it up?
* What's the learning curve?

I think these will be the first three things that I will put my focus on and the rest other things comes to the later.

* Do I really need a heavyweight DB for this application?
```
No, since this is a simple Go webserver, a light wright DB will work. Let's go with SQLite
```
* How simple will it be to set it up?
```
Pretty easy. We can use go-sqlite3 driver for the operations.
```
* What's the learning curve?
```
Since it is a lightweight DB, the learning curve wont be that steep.
```
