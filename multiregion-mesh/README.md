# Multi Regional Mesh Example

## Required Reeading
[K8s Reference Architecture](https://developer.hashicorp.com/consul/tutorials/kubernetes/kubernetes-reference-architecture)

- A consul client exists on certain nodes
- A consul server exists on certain nodes
- Client talks to consul server via RPC
- Consul server Leader talks to Consul server followers via Raft
- Consul client and server communicate via gossip protocol
- In the server section set replicas to 3. This will deploy three servers and cause Consul to wait to perform leader election until all three are healthy.
- Since a Consul client is deployed on every Kubernetes node, you do not need to specify the number of clients for your deployments.
- You have the ability to override the default node reconnect timeout. By default, Consul will wait 72 hours before reaping unresponsive nodes. 
- To enable Consul service mesh, set enabled under the connectInject key to true. In the connectInject section, you can also configure security features. Enabling the default parameter will result in the injector automatically injecting the envoy-sidecar sidecar proxy and consul-sidecar life-cycle sidecar into all pods. 

## Installation
```
helm repo add hashicorp https://helm.releases.hashicorp.com
"hashicorp" has been added to your repositories

Barebones:
helm install consul hashicorp/consul --set global.name=consul --create-namespace -n consul

more defined: (needs triage)
helm upgrade --install consul hashicorp/consul --values config.yaml --create-namespace --namespace consul --version "0.43.0" --wait


helm upgrade --install consul hashicorp/consul --values multiregion-mesh/datacenter-usc1/usc1-dc1.yaml --create-namespace --namespace consul --version "0.43.0" --wait


```
