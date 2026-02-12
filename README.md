## Terraform Enterprise FDO Deployment on Azure using Docker and disk operational mode

This repository provides an automated way to deploy Terraform Enterprise (TFE) on Azure using:
- FDO (Flexible Deployment Options)
- Docker
- Disk operational mode
- Terraform-based infrastructure automation
- AWS Route53 to manage DNS records and handle SSL certificate validation for the Azure virtual machine.

This project automates the entire process, providing a repeatable, consistent, and reliable way to deploy TFE in minutes using Terraform.

## Prerequistes

This guide was executed on MacOS so it assumes the following:
- You have Git installed.
- Azure Credentials are configured.
- AWS Credentials are configured.
- Terraform is installed (tested with Terraform 1.5.7)
- TFE license file


## Clone the repository
- Clone the Github repo
```
git clone https://github.com/mohamed-hashicorp/azure-tfe-fdo-docker-dm-si.git
```
- Change the directory
```
cd azure-tfe-fdo-docker-dm-si
```

## Configure your variables
- Rename the `terraform.tfvars.example`
```
cp terraform.tfvars.example terraform.tfvars
```
- Set the TFE image tag, license and encrytion password
```
ssh_public_key    = "ssh-rsa ..."
data_disk_size_gb = 100
location          = "westeurope"
prefix            = "tfstoragetest"
admin_username    = "azureuser"
subscription_id   = "fc82..."
aws_region        = "eu-west-1"
acme_server_url         = "https://acme-v02.api.letsencrypt.org/directory"
#acme_server_url         = "https://acme-staging-v02.api.letsencrypt.org/directory"
hosted_zone_name        = "mohamed-abdelbaset.sbx.hashidemos.io"
dns_record              = "tfe-azure.mohamed-abdelbaset.sbx.hashidemos.io"
email                   = "mohamedayman@hotmail.com"
tfe_image_tag           = "1.2.0
tfe_license             = "xxx.." # 
tfe_encryption_password = "Mystrongpassword123"
tfe_admin_password      = "Mystrongpassword123"
certs_dir               = "/etc/terraform-enterprise/certs"
data_dir                = "/opt/terraform-enterprise/data"

```

## Create Infrastructure
- Run Terraform init
```
terraform init
```

- Run Terraform apply
```
terraform apply
```

- Type yes if you prompted the following
```
Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value:
```


## Verify
- Check that TFE installation is accessible from your browser.
- Login to `https://tfe-azure.mohamed-abdelbaset.sbx.hashidemos.io/`


## Delete Infrastructure
- When done, you can remove the resources with terraform destroy, type:
```
terraform destroy
```
- Type yes, when prompted:
```
    Do you really want to destroy all resources?
    Terraform will destroy all your managed infrastructure, as shown above.
    There is no undo. Only 'yes' will be accepted to confirm.
    Enter a value:
```