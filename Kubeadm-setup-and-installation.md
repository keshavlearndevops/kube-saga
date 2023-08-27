# Kubeadm Installation Tutorial

This tutorial will help you to setup the Kubernetes Cluster using the Kubeadm

## Pre-requisites

- Ubuntu OS
- sudo privileges
- t2.medium instance type
- Internet access

---

## Commomn commands for Master and Worker Node

Run the below commands on both ***Master*** and ***Worker*** Node for intial setup of kubeadm

```bash
sudo su
sudo apt update
sudo apt-get install -y apt-transport-https ca-certificates curl
sudo apt install docker.io -y

sudo systemctl enable --now docker # enable and start in single command.

# Adding GPG keys.
curl -fsSL "https://packages.cloud.google.com/apt/doc/apt-key.gpg" | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/kubernetes-archive-keyring.gpg

# Add the repository to the sourcelist.
echo 'deb https://packages.cloud.google.com/apt kubernetes-xenial main' | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt update 
sudo apt install kubeadm=1.20.0-00 kubectl=1.20.0-00 kubelet=1.20.0-00 -y
```
Sample command running on Master node

![image](https://github.com/keshavlearndevops/kube-saga/assets/134159375/71138486-7106-4d2a-8917-b364d3e4feac)

![image](https://github.com/keshavlearndevops/kube-saga/assets/134159375/b142753d-c54f-43be-bd65-17ab2b98038e)

![image](https://github.com/keshavlearndevops/kube-saga/assets/134159375/e3e20ee1-bd86-4158-9848-113023230883)

---

## Master Node

1. Initialize the Kubeadm on Master node
```bash
sudo kubeadm init
```
![image](https://github.com/keshavlearndevops/kube-saga/assets/134159375/088086c4-ea0f-461e-8bbd-c141c04402b1)

After running successfully, your Kubernetes control plane will be initialized successfully.

![image](https://github.com/keshavlearndevops/kube-saga/assets/134159375/989f3cab-c9fa-4d79-a12a-aa6b9f37effe)

2. Set up local kubeconfig (both for root user and normal user):

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
![image](https://github.com/keshavlearndevops/kube-saga/assets/134159375/b65b9918-1aac-4f61-b1a1-2840e66cbba6)

3. Apply Weave network:

```bash
kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml
```
![image](https://github.com/keshavlearndevops/kube-saga/assets/134159375/db25b10b-094f-4abe-9b69-4e8d7d3eb4b8)

4. Genetate token to join worker node

```bash
sudo kubeadm token create --print-join-command
```
![image](https://github.com/keshavlearndevops/kube-saga/assets/134159375/3cb57003-0372-45a6-bca0-49a6ac3e9f96)

5. Expose port 6443 in the inbound rules of Master's Security group for the Worker to connect to Master Node

![image](https://github.com/keshavlearndevops/kube-saga/assets/134159375/7600a48d-2bdd-4d1b-b326-31c3182ed7ca)

---

## Worker Node

1. Run the below command on the Worker Node
```bash
sudo kubeadm reset pre-flight checks
```
![image](https://github.com/keshavlearndevops/kube-saga/assets/134159375/2519390c-4d72-4503-8273-417e71216572)

2. Copy amd paste the join command from the master node and append --v=5 at the end of it.

![image](https://github.com/keshavlearndevops/kube-saga/assets/134159375/389a8f48-36df-4456-9a65-79cc010a7a97)

After joining Successfully it shows.

![image](https://github.com/keshavlearndevops/kube-saga/assets/134159375/7d2c894f-572d-4fd4-ac2d-a87729de572f)

---

## Verify Cluster Connection on the Master Node

```bash
kubectl get nodes
```
![image](https://github.com/keshavlearndevops/kube-saga/assets/134159375/e02aefc6-779c-4955-88cf-5cacc5c431a7)

---

## Test a Demo Pod (Optional)

To test a pod, you can run the following command:

```bash
kubectl run hello-world-pod --image=busybox --restart=Never --command -- sh -c "echo 'Hello, World' && sleep 3600"
```
![image](https://github.com/keshavlearndevops/kube-saga/assets/134159375/c63b9df6-75f3-4282-aba8-576d8a84fe6c)










