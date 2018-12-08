# kube-bgo

kube-bgo is an operator for Kubernetes that is attempting to manage the life cycle
of an application using the Blue/Green deployment methodology.

It will ensure that a new `Deployment` is fully rolled out before it is made available
via the `Service`.

## Blue/Green Deployments

The aim of this Operator is to enable the Blue/Green deployment pattern using Kubernetes Deployments. With this Operator you will be adding a `CRD` `BGDeploy` to your Kubernetes Cluster that will create and manage the Kubernetes Resources required to support the Blue/Green deployment pattern.

## Creating a BGDeploy Resource

A `BGDeploy` resource will result in the following Kubernetes resources being created and managed:

- two `Deployment` resources
- two `ConfigMap` resources
- two `Secret` resources
- one `Service` resource

In the `BGDeploySpec` you will define these objects as you would outside of this Operator. In addition to what you define this Operator will add the following `metadata.labels`:

- `Color: (Blue|Green)`
- `ManagedBy: kube-bgo`

When you create the `BGDeploy` resource the `Service` will first target the Label `Color: Green`, the next change will have the `Service` updated to target the Label `Color: Blue`, this will alternate with each change set applied to the `BGDeploy` resource.

Before this target change happens a confirmation of the `Color: Blue` `Deployment` will make sure that it is ready to start handling any connections.

## History of Changes

A history of changes will be maintained on the `BGDeploy` resource so as to allow rolling back any changes made.
