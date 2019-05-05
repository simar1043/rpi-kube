# rpi-kube
scripts to setup raspberry pi kubernetes cluster 

```sh hostname_and_ip.sh k8s-master 192.168.1.100 192.168.1.1```

```sh install.sh```

# kube master node
Run:

```sudo kubeadm init --config kubeadm_conf.yaml```

Output:

```
Your Kubernetes master has initialized successfully!
To start using your cluster, you need to run the following as a regular user:
mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/
You can now join any number of machines by running the following on each node
as root:
kubeadm join --token TOKEN 192.168.1.100:6443 --discovery-token-ca-cert-hash HASH
```

Verify:

```
kubectl get nodes
```

# kube worker node
```
$ sudo kubeadm join --token TOKEN 192.168.1.100:6443 --discovery-token-ca-cert-hash HASH
```

# kube master node setup weave network container

```
kubectl apply -f “https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d ‘\n’)
```
