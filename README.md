# rpi-kube
scripts to setup raspberry pi kubernetes cluster 

```sh hostname_and_ip.sh k8s-master 192.168.1.100 192.168.1.1```

```sh install.sh```

# kube setup 
https://medium.com/nycdev/k8s-on-pi-9cc14843d43

## master node setup

```sudo kubeadm config images pull -v3```

```sudo kubeadm init```

```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

to find token for joining cluster:

```
kubeadm token list
```

sha hash:

```
openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt | openssl rsa -pubin -outform der 2>/dev/null | openssl dgst -sha256 -hex | sed 's/^.* //' 
```

Install the Weave Net network driver:
```
kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"
```

```sudo sysctl net.bridge.bridge-nf-call-iptables=1```

## worker node setup

```
sudo kubeadm join --token <token> <master-node-ip>:6443 --discovery-token-ca-cert-hash sha256:<sha256>
```

```
sudo sysctl net.bridge.bridge-nf-call-iptables=1
```

```
kubectl get nodes
```
