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


Terraform


Install terraform using the link https://developer.hashicorp.com/terraform/install

  wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" |   sudo tee /etc/apt/sources.list.d/hashicorp.list
 sudo apt update && sudo apt install terraform

Create a directory for terraform

main.tf

# Create virtual network
resource "azurerm_virtual_network" "my_terraform_network" {
  name                = "myVnet"
  address_space       = ["10.0.0.0/16"]
  location            = "East US"
  resource_group_name = "user-zjxzssxmersm"
}


providers.tf
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "~>3.0"
    }
    random = {
      source  = "hashicorp/random"
      version = "~>3.0"
    }
  }
}

provider "azurerm" {
  features {}
  skip_provider_registration = "true"
}


variables.tf

variable "resource_group_location" {
  type        = string
  default     = "eastus"
  description = "Location of the resource group."
}

variable "resource_group_name_prefix" {
  type        = string
  default     = "rg"
  description = "Prefix of the resource group name that's combined with a random ID so name is unique in your Azure subscription."
}

