cd C:\VCF-Demo-main
kubectl vsphere login --server 10.80.0.2 --vsphere-username administrator@vsphere.local --insecure-skip-tls-verify
kubectl config use-context namespace-1
kubectl apply -f mysql-vm.yaml
--
- 