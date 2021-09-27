# Prepare Deep Learning environment in Azure with Azure CLI and Ansible

See example environment variables in [`.envrc`](./.envrc).

```bash
# Create a resource group
$ az group create --name ${AZ_RESOURCE_GROUP} --location ${AZ_LOCATION}

# Create a public IP
$ az network public-ip create -g ${AZ_RESOURCE_GROUP} -n ${AZ_PUBLIC_IP}

# How to find an image
# https://docs.microsoft.com/en-us/azure/virtual-machines/linux/cli-ps-findimage

# List VM image publishers
$ az vm image list-publishers --location ${AZ_LOCATION} --output table

# List image offers by publisher `microsoft-dsvm`
$ az vm image list-offers --location ${AZ_LOCATION} --publisher microsoft-dsvm --output table

# List SKUs for publisher `microsoft-dsvm` and offer `linux-data-science-vm-ubuntu`
$ az vm image list-skus --location ${AZ_LOCATION} --publisher microsoft-dsvm --offer linux-data-science-vm-ubuntu --output table

# List images by publisher, offer, and SKU
$ az vm image list \
    --location ${AZ_LOCATION} \
    --publisher microsoft-dsvm \
    --offer linux-data-science-vm-ubuntu \
    --sku linuxdsvmubuntu \
    --all \
    --output table

# Create a virtual machine with chosen image such as
# `microsoft-dsvm:linux-data-science-vm-ubuntu:linuxdsvmubuntu:20.12.11`
# and size such as `Standard_NC6_Promo`
$ az vm create \
  --name ${AZ_VM_NAME} \
  --resource-group ${AZ_RESOURCE_GROUP} \
  --image ${AZ_IMAGE} \
  --location ${AZ_LOCATION} \
  --size ${AZ_SIZE} \
  --ssh-key-value ${AZ_SSH_KEY} \
  --admin-username ${AZ_USER} \
  --public-ip-address ${AZ_PUBLIC_IP} \
  --public-ip-address-allocation static
  # --nsg ${AZ_NSG}

# Find the public IP of the VM
$ az network public-ip show \
  --resource-group ${AZ_RESOURCE_GROUP} \
  --name ${AZ_PUBLIC_IP} \
  --query ipAddress \
  --output json

# List VMs
$ az vm list --output table
# Deallocate VM
$ az vm deallocate -n ${AZ_VM_NAME} -g ${AZ_RESOURCE_GROUP}
# Delete VM
$ az vm delete -g ${AZ_RESOURCE_GROUP} -n ${AZ_VM_NAME}
```

## Ansible

Add `hosts` file based on the example in `hosts.example` and run:

```bash
$ ansible-playbook -i hosts site.yml
```

TODO:
- [ ]  Fix error in starting code-server


## VM commands

```bash
$ nvidia-smi
```
