Testing the High CPU Alert for VM1:

while ($true) { Start-Process taskmgr.exe; Start-Sleep -Milliseconds 100; Stop-Process -Name taskmgr }






Install the LinuxDiagnostic extension in InsightScape-VM2:

1.	Check the version of the waagent:
/usr/sbin/waagent -version
2.	Update and install walinuxagent:
sudo apt-get update && sudo apt-get install walinuxagent
3.	Install wget:
sudo apt-get install -y wget
4.	Install Python 2:
sudo apt-get install -y python2
5.	Set Python 2 as the default Python version:
sudo update-alternatives --install /usr/bin/python python /usr/bin/python2 1
6.	Assign a managed identity to the VM:
az vm identity assign --resource-group InsightScape-RG --name InsightScape-VM2
7.	Download the diagnostics settings JSON file:
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json
8.	Set the diagnostic storage account name:
my_diagnostic_storage_account="insightscapeblob"
9.	Get the resource ID of the VM:
my_vm_resource_id=$(az vm show --resource-group InsightScape-RG --name InsightScape-VM2 --query "id" -o tsv)
10.	Update the diagnostic storage account in the settings file:
sed -i "s#_DIAGNOSTIC_STORAGE_ACCOUNT_#$my_diagnostic_storage_account#g" portal_public_settings.json
11.	Update the VM resource ID in the settings file:
sed -i "s#_VM_RESOURCE_ID_#$my_vm_resource_id#g" portal_public_settings.json
12.	Generate a SAS token for the diagnostic storage account:
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 2037-12-31T23:59:00Z --permissions wlacu --resource-types co --services b --output tsv)
13.	Create the protected settings for the extension:
my_lad_protected_settings="{\"storageAccountName\": \"$my_diagnostic_storage_account\", \"storageAccountSasToken\": \"$my_diagnostic_storage_account_sastoken\"}"
14.	Set the Linux diagnostics extension on the VM:
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 4.0 --resource-group InsightScape-RG --vm-name InsightScape-VM2 --protected-settings "$my_lad_protected_settings" --settings portal_public_settings.json











