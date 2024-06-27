## Install Terraform
```
sudo apt update
sudo apt install software-properties-common gnupg2 curl apt-transport-https ca-certificates

curl https://apt.releases.hashicorp.com/gpg | gpg --dearmor > hashicorp.gpg
sudo install -o root -g root -m 644 hashicorp.gpg /etc/apt/trusted.gpg.d/

sudo apt-add-repository "deb [arch=$(dpkg --print-architecture)] https://apt.releases.hashicorp.com $(lsb_release -cs) main"

sudo apt install terraform
```
## Install Files
```
mkdir classfiles/VCF_demo
mkdir classfiles/TF
cd VCF_demo
git clone https://github.com/KBrookfield/VCF-Demo.git
cd ../TF
git clone https://github.com/mobilegleed/TF.git
```
## Install kubectl
```
sudo apt install unzip
wget <CLI Tools link>
unzip vsphere-plugin.zip
sudo mv bin/* /usr/local/bin
```
 
## Install docker
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
sudo systemctl status docker
sudo usermod -aG docker $USER
```

## Install imgpkg
```
curl -LO https://github.com/carvel-dev/imgpkg/releases/download/v0.42.2/imgpkg-linux-amd64
mv imgpkg-linux-amd64 /usr/local/bin/imgpkg
chmod +x /usr/local/bin/imgpkg
```

## Install vCenter certificates
 ```
wget https://vcenter-wld.vcf.sddc.lab/certs/download.zip --no-check-certificate
unzip download.zip
cd certs/lin
for file in *.0; do mv "$file" "${file%.0}.crt"; done
sudo cp ca.crt /usr/local/share/ca-certificates
sudo update-ca-certificates
```

