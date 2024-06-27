cd C:\VCF-Demo-main
kubectl vsphere login --server 10.80.0.2 --vsphere-username administrator@vsphere.local 
kubectl config use-context namespace-1
kubectl apply -f mysql-vm.yaml
--
## New IaaS Lab for Workshop
cd C:\VCF-Demo-main
kubectl vsphere login --server 10.80.0.2 --vsphere-username administrator@vsphere.local 
kubectl config use-context namespace-1
kubectl apply -f tkg-cc-1.yaml

imgpkg copy -i jswolf059/developer-utilities-backend:latest --to-tar=/tmp/backend.tar
imgpkg copy -i jswolf059/developer-utilities-frontend:latest --to-tar=/tmp/frontend.tar

wget https://harbor.vcf.sddc.lab/api/v2.0/systeminfo/getcert --no-check-certificate
sudo mkdir -p /etc/docker/certs.d/harbor.vcf.sddc.lab/
sudo mv getcert /etc/docker/certs.d/harbor.vcf.sddc.lab/ca.crt

sudo docker login harbor.vcf.sddc.lab
sudo imgpkg copy --tar /tmp/backend.tar --to-repo=harbor.vcf.sddc.lab/3ta/backend --registry-ca-cert-path /etc/docker/certs.d/harbor.vcf.sddc.lab/ca.crt
sudo imgpkg copy --tar /tmp/frontend.tar --to-repo=harbor.vcf.sddc.lab/3ta/frontend --registry-ca-cert-path /etc/docker/certs.d/harbor.vcf.sddc.lab/ca.crt

kubectl vsphere login --server 10.80.0.2 --vsphere-username administrator@vsphere.local
kubectl config use-context namespace-1
kubectl apply -f mysql-vm.yaml

kubectl get service
echo -n "<IP of mysql-vm service>" | base64 -w 0

nano backend-app.yaml

kubectl vsphere login --server 10.80.0.2 --tanzu-kubernetes-cluster-name tkg-cc-1 --tanzu-kubernetes-cluster-namespace namespace-1 --vsphere-username administrator@vsphere.local
kubeclt get nodes

kubectl create ns app-ns
kubectl label --overwrite ns --all pod-security.kubernetes.io/enforce=privileged
kubectl create secret docker-registry docker-hub-creds --docker-server=harbor.vcf.sddc.lab --docker-username=admin --docker-password=Harbor12345 -n app-ns
kubectl apply -f backend-app.yaml -n app-ns
kubectl get pod -n app-ns
kubectl get service -n app-ns

curl -X GET BackendServiceIP:5000/api/index
echo -n “BackendServiceIP:5000” |base64 -w 0

nano frontend-app.yaml

kubectl apply -f frontend-app.yaml -n app-ns
kubectl get pod -n app-ns
kubectl get service -n app-ns

