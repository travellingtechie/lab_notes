## How to ssh to kubernetes node
```
kubectl get vm -o wide
kubectl get secrets
```
## Setting up Aria Ops with Kubernetes
- Get kubeconfig (includes creds for Aria Ops)
  - kubectl get secrets "tkc-cc-a-kubeconfig -o jsonpath='{.data.value}' | base64 -d
- Get Yaml for cAdvisor (https://docs.vmware.com/en/VMware-Aria-Operations-for-Integrations/2.1/Management-Pack-for-Kubernetes/GUID-13C06790-C129-4547-B81C-FDCA2BEB29BC.html)
- kubectl create -f cadvisor.yaml
- kubectl get cluster-info 
- Install kubernetes management pack (in dropbox)
- Integrations > Cloud Account Info
  - Name: cluster name
  - Control panel URL
  - Collector Service: cAdvisor - DaemonSet
  - port 31194
  - creds from kubeconfig
  - 