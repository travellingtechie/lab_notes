## Aria Auto
## vCenter-WLD Prerequisites
- Create VM Folder: Production
- Download and add Ubuntu-18.04 to Content Library

## NSX-WLD
- Create prod-net
  - 192.168.64.1/18
  - No DHCP


## Aria Automation without Quickstart
- Add Cloud Account
  - VCF
    - VLC-Holo-Site-1-WLD1
      - WLD-01
      - Use vCenter and NSX Creds
      - Add env:prod and env:dev tags
- Cloud Zone
  - Add Folder: Production
  - Add Tags:  env:dev env:prodprod-net
- New Project
  - VLC Holodeck
  - Add Users

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
    - Network Policies
      - T0
      - Add Edge Cluster
- IP Range
  - Prod IP Range
    - 192.168.66.100-192.168.67.200
- Integrations
  - Add Aria Operations

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
- Integrations
  - VMware Infrastructure Health
  - Logs
- Install Cloud Proxy
- Cloud Accounts
  - vCenter
  - NSX

## Aria Auto Integrations
- Aria Ops

## Aria Logs
- Integrations
  - Ops
- Content Packs
  - NSX
  - Aria Ops
  - Aria Automation
- Add vCenters
- Add NSX

## Deploy Shopping Cart App

## VVS
- Power CLI
```
Set-PSRepository -Name PSGallery -InstallationPolicy Trusted 
Install-Module -Name VMware.PowerCLI -MinimumVersion 13.1.0 
Install-Module -Name VMware.vSphere.SsoAdmin -MinimumVersion 1.3.9 
Install-Module -Name PowerVCF -MinimumVersion 2.4.0 
Install-Module -Name PowerValidatedSolutions -MinimumVersion 2.8.0 
Install-Module -Name VMware.CloudFoundation.PasswordManagement MinimumVersion 1.7.0
Install-Module -Name VMware.CloudFoundation.Reporting -MinimumVersion 2.6.0

Set-PowerCLIConfiguration -Scope AllUsers -ParticipateInCEIP $false Confirm:$false
Import-Module-Name VMware.PowerCLI 
Import-Module-Name VMware.vSphere.SsoAdmin 
Import-Module-Name PowerVCF 
Import-Module-Name PowerValidatedSolutions 
Import-Module-Name VMware.CloudFoundation.PasswordManagement
Import-Module -Name VMware.CloudFoundation.Reporting
```

Verify that the required modules are installed
```
Test-VcfPasswordManagementPrereq
Test-VcfReportingPrereq
```

