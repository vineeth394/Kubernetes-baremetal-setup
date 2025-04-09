# Kubernetes-baremetal-setup

**Save the below files and run in Msster and Worker**

 bash ./container.sh

 bash ./kube.sh


 **In Master Only**

1.kubeadm init --pod-network-cidr=10.244.0.0/16

After Kubeadm init you will get kubeadm join command, copy it and save - this is unique - this is needed later
**do not run this**
kubeadm join 172.31.12.83:6443 --token c4p4o9.wka20bm8zobf0cti \
        --discovery-token-ca-cert-hash sha256:146841827f6abc8f428b6d9e814ef517315b88403e81c1f293e322cf8bfabd34

2.mkdir -p $HOME/.kube 

3.sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config 

4.sudo chown $(id -u):$(id -g) $HOME/.kube/config 

5.export KUBECONFIG=/etc/kubernetes/admin.conf 

6. kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml 

**Enable PORTs in All EC2 instances - all traffic both inbound and outbound**

**In Wokrer Node Only**
You can now join any number of machines by running the following on each node as root: 

kubeadm join <control-plane-host>:<control-plane- 
port> --token <token> --discovery-token-ca-cert-hash  
sha256:<hash> 

Ex:
kubeadm join 172.31.12.83:6443 --token c4p4o9.wka20bm8zobf0cti \
        --discovery-token-ca-cert-hash sha256:146841827f6abc8f428b6d9e814ef517315b88403e81c1f293e322cf8bfabd34

**To Check Connection is Successful:**
kubectl get pods -A
kubectl get nodes
kubectl get pods -A -owide #owide option displays ip address 
kubectl get nodes -owide 
