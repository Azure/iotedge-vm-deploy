# iotedge-vm-deploy

Detailed documentation is available on [Microsoft Docs](https://docs.microsoft.com/en-us/azure/iot-edge/how-to-install-iot-edge-ubuntuvm)

## ARM Template to deploy IoT Edge enabled VM

The following Azure Resource Templates are for IoT Edge release 1.4.

ARM template to deploy a VM with IoT Edge pre-installed (via cloud-init)

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fiotedge-vm-deploy%2Fmaster%2FedgeDeploy.json" target="_blank">
    <img src="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.png" />
</a>

The ARM template visualized for exploration

<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fiotedge-vm-deploy%2Fmaster%2FedgeDeploy.json" target="_blank">
    <img src="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/visualizebutton.png" /></a>

## Azure CLI command to deploy IoT Edge enabled VM 

The commands below deploy a VM with IoT Edge pre-installed **and provisioned** with the provided connection string. To deploy a VM with IoT Edge pre-installed but **not provisioned**, do not include the `--parameters deviceConnectionString=...` portion of the command.

### Using an ARM template

```bash
az group deployment create \
  --name edgeVm \
  --resource-group replace-with-rg-name \
  --template-uri "https://raw.githubusercontent.com/Azure/iotedge-vm-deploy/master/edgeDeploy.json" \
  --parameters dnsLabelPrefix='my-edge-vm1' \
  --parameters adminUsername='azureuser' \
  --parameters authenticationType='sshPublicKey' \
  --parameters adminPasswordOrKey="$(< ~/.ssh/id_rsa.pub)" \
  --parameters deviceConnectionString=$(az iot hub device-identity show-connection-string --device-id replace-with-device-name --hub-name replace-with-hub-name -o tsv)
```

### Using an Azure Bicep file

```bash
az group deployment create \
  --name edgeVm \
  --resource-group replace-with-rg-name \
  --template-file "https://raw.githubusercontent.com/Azure/iotedge-vm-deploy/master/edgeDeploy.bicep" \
  --parameters dnsLabelPrefix='my-edge-vm1' \
  --parameters adminUsername='azureuser' \
  --parameters authenticationType='sshPublicKey' \
  --parameters adminPasswordOrKey="$(< ~/.ssh/id_rsa.pub)" \
  --parameters deviceConnectionString=$(az iot hub device-identity show-connection-string --device-id replace-with-device-name --hub-name replace-with-hub-name -o tsv)
```

# Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.opensource.microsoft.com.

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
