# Sprint 1
TODO: Student to complete code and comments in the sections below.

## Install Kubernetes node 1

- Customized kubeadm-config.yaml:
$ cat /tmp/kubeadm-config.yaml 
kind: InitConfiguration
apiVersion: kubeadm.k8s.io/v1beta3
bootstrapTokens:
- token: ipmycx.ku9jvun6f34lo5aq
nodeRegistration:
  ignorePreflightErrors:
  - NumCPU
---
kind: JoinConfiguration
apiVersion: kubeadm.k8s.io/v1beta3
discovery:
  bootstrapToken:
    apiServerEndpoint: hol11:6443
    token: ipmycx.ku9jvun6f34lo5aq
    unsafeSkipCAVerification: true
nodeRegistration:
  ignorePreflightErrors:
  - NumCPU
---
kind: KubeletConfiguration
apiVersion: kubelet.config.k8s.io/v1beta1
failSwapOn: false
---
kind: ClusterConfiguration
apiVersion: kubeadm.k8s.io/v1beta3
apiServer:
  certSANs:
  - 35.87.153.76




[35.87.153.76] (kubernetes-admin@kubernetes:N/A) k8s@hol11 ~
$ kubectl create namespace hello
namespace/hello created
[35.87.153.76] (kubernetes-admin@kubernetes:N/A) k8s@hol11 ~
$ kubectl get namespace hello -o yaml
apiVersion: v1
kind: Namespace
metadata:
  creationTimestamp: "2023-08-11T03:09:48Z"
  labels:
    kubernetes.io/metadata.name: hello
  name: hello
  resourceVersion: "2180"
  uid: 8daa8d65-d6e0-4f53-9689-4ba20ebe218f
spec:
  finalizers:
  - kubernetes
status:
  phase: Active
[35.87.153.76] (kubernetes-admin@kubernetes:N/A) k8s@hol11 ~
$ kubectl get namespaces --show-labels -w
NAME              STATUS   AGE   LABELS
default           Active   22m   kubernetes.io/metadata.name=default
hello             Active   19s   kubernetes.io/metadata.name=hello
kube-node-lease   Active   22m   kubernetes.io/metadata.name=kube-node-lease
kube-public       Active   22m   kubernetes.io/metadata.name=kube-public
kube-system       Active   22m   kubernetes.io/metadata.name=kube-system
^C[35.87.153.76] (kubernetes-admin@kubernetes:N/A) k8s@hol11 ~
$ kubectl get pods --watch --output-watch-events
