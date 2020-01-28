This repository has a few sample resource files in K8's.

Initializing Kubernetes cluster using kubeadm:

# aws.yml
---
apiVersion: kubeadm.k8s.io/v1beta2
kind: ClusterConfiguration
networking:
  serviceSubnet: "10.100.0.0/16"
  podSubnet: "10.244.0.0/16"
apiServer:
  extraArgs:
    cloud-provider: "aws"
controllerManager:
  extraArgs:
    cloud-provider: "aws"
    
_-----------------------------    
    
initialize cluster using following command:

---> kubeadm init — config /etc/kubernetes/aws.yml

#node.yml

---
apiVersion: kubeadm.k8s.io/v1beta1
kind: JoinConfiguration
discovery:
  bootstrapToken:
    token: "rat2th.qzmvv988e3pz9ywa"
    apiServerEndpoint: "10.0.0.102:6443"
    caCertHashes:
      - "sha256:ce983b5fbf4f067176c4641a48dc6f7203d8bef972cb9d2d9bd34831a864d744"
nodeRegistration:
  name: ip-10-0-0-186.eu-west-3.compute.internal
  kubeletExtraArgs:
    cloud-provider: aws
    
 join node to the cluster using this command:
 ---> kubeadm join — config /etc/kubernetes/node.yml
 
 
 
    
    
