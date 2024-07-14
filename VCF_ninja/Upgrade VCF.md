- Update vSAN HCL DB7CD9__GUID-17B01B05-8AB0-4539-B722-4B5A706A42F4
- Download Bundle Transfer Utility from VMware
  - I have it in Dropbox  https://www.dropbox.c
  - https://docs.vmware.com/en/VMware-Cloud-Foundation/5.1/vcf-lifecycle/GUID-2E70DA12-2DF3-456D-88C2-21BB35876AB1.html#GUID-5CFB2BBF-7CF6-4003-8CC9-A3AF401Com/scl/fi/v246qopwdchrjcz0pyx9x/lcm-tools-prod.tar.gz?rlkey=2rhdxdfx360x3zjvnj2htnb8y&dl=1
  - JSON file: https://www.dropbox.com/scl/fi/v60co0i8b2avgh6e430nu/vsan_db.json?rlkey=ig89ehafhtpae1gowa07rcf35&dl=1

## Prepare for Upgrade
### Enable auto retry on SDDC Manager
```
vi /opt/vmware/vcf/lcm/lcm-app/conf/application-prod.properties
systemctl restart lcm
```

### Enable FTP on holoconsole
- Server Manager > Manager > Add Roles
  - Add FTP under IIS
- Server Manager > Tools > Computer Management
