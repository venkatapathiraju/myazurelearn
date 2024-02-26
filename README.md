Creating a storage account

  LRS, Storage V2 

set randomnum

stroageAcctName = "storage"$randomNum

az storage account create -n $storageAccountName --resource-group $resource --sku Standard_LRS

Can we automate this with Terraform
configure network access to azure storage
  Enabled from selected virtual networks and IP addresses


Create Container under storage account

SMB Fileshare
