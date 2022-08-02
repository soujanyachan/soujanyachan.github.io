# chapter 11 - undeerstanding kubernetes internals
cluster is split into the kubernetes control plane and the worker nodes

control plane components
- etcd distributed persistent storage
- API server
- scheduler
- controller manager

worker node components
- kubelet
- kube-proxy
- container runtime

add-on components
- DNS
- dashboard
- ingress controller
- heapster
- container network interface plugin

how the components communicate
- 
