# Prepare Deep Learning environment in Azure

```bash
$ az group create --name ${AZ_RESOURCE_GROUP} --location ${AZ_LOCATION}
$ az vm create \
  --name ${AZ_VM_NAME} \
  --resource-group ${AZ_RESOURCE_GROUP} \
  --image ${AZ_IMAGE} \
  --location ${AZ_LOCATION} \
  --size ${AZ_SIZE} \
  --ssh-key-value ${AZ_SSH_KEY} \
  --admin-username ${AZ_USER}
  # --nsg ${AZ_NSG}
# List VMs
$ az vm list --output table
# Deallocate
$ az vm deallocate -n ${AZ_VM_NAME} -g ${AZ_RESOURCE_GROUP}
# Delete VM
$ az vm delete -g ${AZ_RESOURCE_GROUP} -n ${AZ_VM_NAME}
```

## [Find images](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/cli-ps-findimage)

```bash
# List publishers
$ az vm image list-publishers --location ${AZ_LOCATION} --output table
# List offers by publisher
$ az vm image list-offers --location ${AZ_LOCATION} --publisher microsoft-dsvm --output table
# List SKUs by publisher and offer
$ az vm image list-skus --location ${AZ_LOCATION} --publisher microsoft-dsvm --offer linux-data-science-vm-ubuntu
# List images by publisher, offer, and SKU
$ az vm image list \
    --location ${AZ_LOCATION} \
    --publisher microsoft-dsvm \
    --offer linux-data-science-vm-ubuntu \
    --sku linuxdsvmubuntu \
    --all \
    --output table
```

## Image commands

```bash
$ nvidia-smi
```