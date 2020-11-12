# memcached-operator
memcached-operator from Operator SDK quickstart gor Go based operator

## Install and create Operator GO SDK

### Create ubuntu server
multipass launch --name ubuntu18server 18.04 \
multipass shell ubuntu18server

### Prerequisites
( https://sdk.operatorframework.io/docs/installation/install-operator-sdk/#prerequisites ) \
https://docs.docker.com/engine/install/ubuntu/ \
https://kubernetes.io/docs/tasks/tools/install-kubectl/

### Install operator framework sdk
https://sdk.operatorframework.io/docs/installation/install-operator-sdk/#install-from-github-release

### Other prerequisites
sudo snap install go –classic \
sudo apt-get install mercurial \
sudo apt install make \
sudo apt-get install build-essential

### Kubebuilder prerequisites
os=$(go env GOOS) \
arch=$(go env GOARCH) \
curl -L https://go.kubebuilder.io/dl/2.3.1/${os}/${arch} | tar -xz -C /tmp/ \
sudo mv /tmp/kubebuilder_2.3.1_${os}_${arch} /usr/local/kubebuilder \
export PATH=$PATH:/usr/local/kubebuilder/bin

### Quickstart go-based operator
https://sdk.operatorframework.io/docs/building-operators/golang/quickstart/

### other prerequisites (again)
https://book.kubebuilder.io/quick-start.html#installation \
sudo snap install kustomize

# Golang Based Operator Tutorial - notes

## What’s in a basic project?

When scaffolding out a new project, Kubebuilder provides us with a few basic pieces of boilerplate. \
First up, basic infrastructure for building your project: \
- go.mod: A new Go module matching our project, with basic dependencies
- Makefile: Make targets for building and deploying your controller
- PROJECT: Kubebuilder metadata for scaffolding new components

We also get launch configurations under the config/ directory. Right now, it just contains Kustomize YAML definitions required to launch our controller on a cluster, but once we get started writing our controller, it’ll also hold our CustomResourceDefinitions, RBAC configuration, and WebhookConfigurations. \
config/default contains a Kustomize base for launching the controller in a standard configuration. \

Each other directory contains a different piece of configuration, refactored out into its own base: \
- config/manager: launch your controllers as pods in the cluster
- config/rbac: permissions required to run your controllers under their own service account

Last, but certainly not least, Kubebuilder scaffolds out the basic entrypoint of our project: main.go. Let’s take a look at that next...

## Operators Scope

A namespace-scoped operator watches and manages resources in a single Namespace, whereas a cluster-scoped operator watches and manages resources cluster-wide. \
An operator should be cluster-scoped if it watches resources that can be created in any Namespace. An operator should be namespace-scoped if it is intended to be flexibly deployed. This scope permits decoupled upgrades, namespace isolation for failures and monitoring, and differing API definitions. \
By default, operator-sdk init scaffolds a cluster-scoped operator. This document details conversion of default operator projects to namespaced-scoped operators. Before proceeding, be aware that your operator may be better suited as cluster-scoped. For example, the cert-manager operator is often deployed with cluster-scoped permissions and watches so that it can manage and issue certificates for an entire cluster.

# THEORY

## What are Operators?
More technically, Operators are a method of packaging, deploying, and managing a Kubernetes application.

## Why use Operators?
Operators provide:
- Repeatability of installation and upgrade.
- Constant health checks of every system component.
- Over-the-air (OTA) updates for OpenShift components and ISV content.
- A place to encapsulate knowledge from field engineers and spread it to all users, not just one or two.


# Operator Best Practices (community operators)

## Development
An Operator should manage a single type of application, essentially following the UNIX principle: do one thing and do it well. \
If an application consists of multiple different tiers or components, multiple Operators should be written for each of them. If the application for example consists of Redis, AMQ and MySQL, there should be 3 Operators, not one. \
CRD can only be owned by a single Operator, shared CRDs should be owned by a separate Operator

## Running On-Cluster
Like all containers on Kubernetes, Operators shouldn’t need to run as root unless absolutely necessary. Operators should come with their own ServiceAccount and not rely on the default. \
Operators should not self-register their CRDs. These are global resources and careful consideration needs to be taken when setting those up. Also this requires the Operator to have global privileges which is potentially dangerous compared to that little extra convenience. \
An Operator should not deploy another Operator - an additional component on cluster should take care of this (OLM). \
