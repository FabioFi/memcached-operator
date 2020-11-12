# memcached-operator
memcached-operator from Operator SDK quickstart gor Go based operator

## Install and create Operator GO SDK

### Create ubuntu server
multipass launch --name ubuntu18server 18.04
multipass shell ubuntu18server

### Prerequisites
( https://sdk.operatorframework.io/docs/installation/install-operator-sdk/#prerequisites )
https://docs.docker.com/engine/install/ubuntu/
https://kubernetes.io/docs/tasks/tools/install-kubectl/

### Install operator framework sdk
https://sdk.operatorframework.io/docs/installation/install-operator-sdk/#install-from-github-release

### Other prerequisites
sudo snap install go –classic
sudo apt-get install mercurial
sudo apt install make
sudo apt-get install build-essential

### Kubebuilder prerequisites
os=$(go env GOOS)
arch=$(go env GOARCH)
curl -L https://go.kubebuilder.io/dl/2.3.1/${os}/${arch} | tar -xz -C /tmp/
sudo mv /tmp/kubebuilder_2.3.1_${os}_${arch} /usr/local/kubebuilder
export PATH=$PATH:/usr/local/kubebuilder/bin

### Quickstart go-based operator
https://sdk.operatorframework.io/docs/building-operators/golang/quickstart/




# Golang Based Operator Tutorial

## What’s in a basic project?

When scaffolding out a new project, Kubebuilder provides us with a few basic pieces of boilerplate.
First up, basic infrastructure for building your project:
- go.mod: A new Go module matching our project, with basic dependencies
- Makefile: Make targets for building and deploying your controller
- PROJECT: Kubebuilder metadata for scaffolding new components

We also get launch configurations under the config/ directory. Right now, it just contains Kustomize YAML definitions required to launch our controller on a cluster, but once we get started writing our controller, it’ll also hold our CustomResourceDefinitions, RBAC configuration, and WebhookConfigurations.
config/default contains a Kustomize base for launching the controller in a standard configuration.

Each other directory contains a different piece of configuration, refactored out into its own base:
- config/manager: launch your controllers as pods in the cluster
- config/rbac: permissions required to run your controllers under their own service account

Last, but certainly not least, Kubebuilder scaffolds out the basic entrypoint of our project: main.go. Let’s take a look at that next...




