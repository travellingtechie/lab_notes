```
cd C:\VCF-ValidatedSolutions\

$PSVersionTable
Test-VcfPasswordManagementPrereq

$policyFile = "PasswordPolicyConfig.json"
Get-PasswordPolicyDefault -generateJson -jsonFile passwordPolicyConfig.json -version 5.1.0.0

$sddcManagerFqdn = "sddc-manager.vcf.sddc.lab"
$sddcManagerUser = "administrator@vsphere.local"
$sddcManagerPass = "VMware123!"
$sddcRootPass = "VMware123!"
$reportPath = "C:\VCF-ValidatedSolutions" 
$policyFile = "PasswordPolicyConfig.json"

Invoke-PasswordPolicyManager -sddcManagerFqdn $sddcManagerFqdn -sddcManagerUser $sddcManagerUser -sddcManagerPass $sddcManagerPass -sddcRootPass $sddcRootPass -reportPath $reportPath -allDomains -drift -policyFile $policyFile

Start-PasswordPolicyConfig -sddcManagerFqdn $sddcManagerFQDN -sddcManagerUser $sddcManagerUser -sddcManagerPass $sddcManagerPass -sddcRootPass $sddcRootPass -reportPath $reportPath -policyFile $policyFile

Invoke-PasswordPolicyManager -sddcManagerFqdn $sddcManagerFqdn -sddcManagerUser $sddcManagerUser -sddcManagerPass $sddcManagerPass -sddcRootPass $sddcRootPass -reportPath $reportPath -allDomains -drift -policyFile $policyFile

Test-VcfReportingPrereq
$sddcManagerLocalUser = "root"
$sddcManagerLocalPass = "VMware123!"

Invoke-VcfHealthReport -sddcManagerFqdn $sddcManagerFqdn -sddcManagerUser $sddcManagerUser -sddcManagerPass $sddcManagerPass -sddcManagerLocalUser $sddcManagerLocalUser -sddcManagerLocalPass $sddcManagerLocalPass -reportPath $reportPath -allDomains -failureOnly

```