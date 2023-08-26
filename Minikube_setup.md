# Minikube Setup and Installation Guide for Ubuntu OS

This tutorial will give you step by step instructions for Minikube installation. Minikube is easy for single node configuration, where both Master and Worker is on the same server. It is good for Learning Purpose.

## Pre-requisites
- Ubuntu OS
- t2.medium instance trype if using AWS
- Internet Access
- Virtualization must be enabled, if using in local machine

  ---

  ## Step 1: Update the System Packages

 Update your packages to the latest dependencies for better performance and upgraded features or bug fixes.

 ```bash
sudo apt update -y
```

![image](https://github.com/keshavlearndevops/kube-saga/assets/134159375/4811c300-3d1d-4486-a576-e345af50eac6)

---

 ## Step 2: Installing Required Packages

 Installing one of the required package

 ```bash
sudo apt install -y curl wget apt-transport-https
```

![image](https://github.com/keshavlearndevops/kube-saga/assets/134159375/0892929a-5532-4042-9365-232a126c3598)

---

## Step 3: Installing Docker

The K8s needs a container runtime, you can use a VM  or locally. We are using local method using docker

```bash
sudo apt install -y docker.io
```

![image](https://github.com/keshavlearndevops/kube-saga/assets/134159375/a2c15c6d-d0e9-4bb1-88e2-b135e604f1b4)

 ***Start and Enable Docker***
 ```bash
 sudo systemctl enable --now docker
```

Add User to the docker group to remove the sudo overhead

```bash
sudo usermod -aG docker $USER && newgrp docker
```
Now reboot your system and connect again

```bash
sudo reboot
```

---

## Step 4: Installing Minikube

First we will download the Minikube binary using `curl`
```bash
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```

Now make it executable and move to your bin path

```bash
chmod +x minikube
sudo mv minikube /usr/local/bin/
```

![image](https://github.com/keshavlearndevops/kube-saga/assets/134159375/51c74c6b-838d-4971-8b17-f2d52769c17a)

---

## Step 5: Install Kubectl

Kubectl is a command line tool which helps in interracting and sending commands to the the k8s.

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

Make it executable and move it into your path

```bash
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
```

![image](https://github.com/keshavlearndevops/kube-saga/assets/134159375/741d4195-90a3-4335-947b-bfc8755b622f)

---

## Step 6: Start Minikube

Start the Minikube using the below command.

```bash
minikube start --driver=docker
```

![image](https://github.com/keshavlearndevops/kube-saga/assets/134159375/f79bdb88-b254-4cb9-92f1-5b1fe97f87ab)

---

## Step 7: Check the cluster status

Check the cluster status with:

```bash
minikube status
docker ps
```

![image](https://github.com/keshavlearndevops/kube-saga/assets/134159375/4f03e51f-7f6c-45d1-8bd3-673b527cd678)

You can start practising k8s now

---

## Step 8: Stop the Minikube

When you are done, you may stop the minikube or may delete it afterwards

```bash
minikube stop
minikube delete
```

![image](https://github.com/keshavlearndevops/kube-saga/assets/134159375/8b0f9b59-369d-485e-b071-80a5d26f791b)

---

You've successfully installed Minikube on Ubuntu, and you can now start practising k8s, deploy pods or anything you like to do with it.
