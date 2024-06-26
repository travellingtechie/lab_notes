## vCenter-MGMT Prerequisites
- Create VM Folder: Recovered VMs

## NSX-MGMT
- Create prod-net

## vCenter-WLD Prerequisites
- Create VM Folder: Production
- Download and add Ubuntu-18.04 to Content Library

## NSX-WLD
- Create prod-net
  - 192.168.64.1/18
  - No DHCP

## Active Directory
- Add users (need firstname, lastname, email)
  - vcfuser
  - vcfapprover
  - update administrator with first/last/email
- Add Groups
  - vcfuser
  - vcfapprover
 
## vIDM
Administration Console > Identity and Access Management
- Add Active Directory
  - vcf.holo.lab
    - Does not support DNS Service Location
    - 10.0.0.2
    - dc=vcf,dc=holo,dc=lab
    - cn=administrator,cn=users,dc=vcf,dc=holo,dc=lab
    - VMware123!
  - vcf.holo.lab
    - Specify the group DNs:  dc=vcf,dc=holo,dc=lab
      - Administrators, Users
    - User DNs: cn=users,dc=vcf,dc=holo,dc=lab


## Aria Automation without Quickstart
- Hide Quickstart page
- Assembler > Infrastructure > Cloud Account
- Add Cloud Account
  - vCenter
    - vcenter-wld
    - administrator@vsphere.local
    - tags: env:prod env:dev site:ny site:la
  - NSX
    - nsx-wld
    - admin
    - tags: env:prod
 - Cloud Zone
  - Add Folder: Production
  - Add Tags:  env:dev env:prodprod-net
- New Project
  - VLC Holodeck
  - Add Users
    - vcfuser
      - member, viewer
    - vcfapprover
      - viewer, supervisor
## Kubernetes Configuration
- Resources > Supervisors > Add Supervisor Cluster
  - accoutn: vcenter-wld
  - supervisor cluster: wld01-c01
- resources > Supervisors > New Supervisor Namespace
  - Name: aria-namespace
  - account: vcenter-wld
  - supervisor Cluster
- Kubernetes Zone
  - Account: vcenter-wld
  - Name: vcenter-wld-k8s
  - tags: env:prod env:dev
  - Provisioning
    - Add Compute
      - Compute: wld01-c01
      - aria-namespace
- Project > VLC Holodeck > Kubernetes Provisioning
  - Add k8s
- Configure > Cluster Plans
  - New Cluster Plan
    - Account: vcenter-wld
    - Name: vcenter-wld-k8s-cluster-plan
    - version 1.26
    - Control plane 1 best-effort-small
    - Workers: 2 best-effort-small

## Customize Cloud Assembly

- Create Flavor Mappings
  - small 1,1,1
  - medium 1,2,2
  - large 2,2,2
- Create Image Mappings
  - ubuntu-2204
  - ubuntu-1804
- Network Profiles
  - prod-net
    - tag: net:web, net:db
    - Network: prod-net
      - domain: vcf.sddc.lab
      - dns: 8.8.8.8
    - IP Range
      - Prod IP Range
      - 192.168.66.100-192.168.67.200
    - Network Policies
      - T0
      - Add Edge Cluster



## Add Templates
- https://tinyurl.com/cu5uu4fr
  - Shopping Cart App
    - Update passwords
    - update imageref
- Web Server
  - Update password
- Hybrid Shopping Cart App
    - Update passwords
    - update image

## Aria Ops
- Cloud Accounts
  - Cloud Foundation
    - sddc-manager.vcf.sddc.lab
    - Validate vCenter, vSAN, NSX for each WLD
    - Activate Service Discovery, No permissions
- 
- Data Sources > Integrations > Repository
  - VMware Infrastructure Health
  - Aria Automation?
  - Aria Operations for Logs
  - OS and Applicaiton Monitoring
  - NSX
  - Aria Automation Orchestrator
  - SDDC Health MOnitoring
- ssh to 10.0.0.221
  - Edit /etc/maradns/db.vcf.sddc.lab
    - add aria-cloud-proxy.vcf.sddc.lab FQDN4 10.0.0.13
  - systemctl restart maradns
  - logout
- Install Cloud Proxy
  - Download VM from Aria Ops
  - Copy Key
  - Deploy OVA in mgmt WLD
    - aria-cloud-proxy
    - ntp: 10.0.0.221
    - Static IP
    - IP: 10.0.0.13
    - Gateway: 10.0.0.221


## Aria Auto Integrations
- Integrations
  - Add Aria Operations
    - name: vlc-aria-ops
    - url: https://aria-ops.vcf.sddc.lab/suite-api
    - no capabilities tags?

## Aria Logs
- vCenter Integration
  - vcenter-mgmt.vcf.sddc.lab
  - vcenter-wld.vcf.sddc.lab
- Integrations
  - Ops
    - aria-ops.vcf.sddc.lab
- Content Packs
  - NSX
  - Aria Ops
  - Aria Automation

## NSX for Aria Logs
- NSX Mgrs, edges
  - ssh
```
set logging-server aria-logs.vcf.sddc.lab proto udp level info
```
This didnt' work


## Deploy Shopping Cart App

## VVS
- Power CLI
```
install-psresource
Set-PSRepository -Name PSGallery -InstallationPolicy Trusted 
Install-Module -Name VMware.PowerCLI -MinimumVersion 13.1.0 
Install-Module -Name VMware.vSphere.SsoAdmin -MinimumVersion 1.3.9 
Install-Module -Name PowerVCF -MinimumVersion 2.4.0 
Install-Module -Name PowerValidatedSolutions -MinimumVersion 2.8.0 
Install-Module -Name VMware.CloudFoundation.PasswordManagement -MinimumVersion 1.7.0
Install-Module -Name VMware.CloudFoundation.Reporting -MinimumVersion 2.6.0

Set-PowerCLIConfiguration -Scope AllUsers -ParticipateInCEIP $false -Confirm:$false
Import-Module -Name VMware.PowerCLI 
Import-Module -Name VMware.vSphere.SsoAdmin 
Import-Module -Name PowerVCF 
Import-Module -Name PowerValidatedSolutions 
Import-Module -Name VMware.CloudFoundation.PasswordManagement
Import-Module -Name VMware.CloudFoundation.Reporting
```

Verify that the required modules are installed
```
Test-VcfPasswordManagementPrereq
Test-VcfReportingPrereq
```

## NSX Segment for L2VPN
- WLD 
- Create T1 DHCP Profile
- Add DHCP profile to T1
- Create dev-nit Segment
  - 192.168.128.1/18
  - DHCP
  - 192.168.128.100-192.168.128.199
  - DNS 10.0.0.221
- MGMT WLD
  - Create L2E_dev-net
  - No gateway
  - No DHCP


## Aria Automation Catalog
- Start > Identity and Access Management
  - Add roles to vcfuser and vcfapprover
- Assembler > Design
  - Create version of all apps (if not done)
  - check box to release to catalog
- Service Broker > Content & Policies
  - New Content Source
    - Name: VLC Holodeck Templates
    - Source Project: VLC Holodeck project
- Polices > Definitions > New Content Sharing Policy
  - VLC Holodeck
  - Scope: VLC Holodeck
  - Add Content Source
  - Users
    - vcfuser
    - vcfapprover
- Add Approvcal Policy
  - Name: VLC Holodeck Approval Policy
  - Scope: VLC Holodeck
  - Criteria: Template equals Hybrid Shopping Cart App
  - Approvers: vcf approver
  - Actions: Deployment.Create Cloud.vSphere.Machine.Add.Disk

## vCenter Changes for vMotion
- Add advanced parameter to allow vMotion between vDSs
  - config.vpxd.network.allowVmotionBetweenLogicalSwitches  True

## Deploy Ubuntu-VM
- Create ubuntu customization specification
- Deploy ubuntu-vm1
- Deploy ubuntu-vm2

## Changes for VCSR Labs (moved these to appropriate spot above)
- MGMT NSX  (Save this for lab)
  - add dev-net
  - add prod-net
- MGMT vCenter
  - Create Folders
    - Recovered VMs
  - Create Resource Pool
    - Recovered VMs
- Update from https://github.com/KBrookfield/VCF-Demo