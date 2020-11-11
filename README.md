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


