# kube-bgo

kube-bgo is an operator for Kubernetes that is attempting to manage the life cycle
of an application using the Blue/Green deployment methodology.

It will ensure that a new `Deployment` is fully rolled out before it is made available
via the `Service`.