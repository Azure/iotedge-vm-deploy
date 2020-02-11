# edge-vm-deploy
ARM template to deploy a VM with IoT Edge pre-installed (via cloud-init)

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fveyalla%2Fedge-vm-deploy%2Fmaster%2FedgeDeploy.json" target="_blank">
    <img src="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.png" />
</a>

The ARM template visualized for exploration

<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2Fveyalla%2Fedge-vm-deploy%2Fmaster%2FedgeDeploy.json" target="_blank">
    <img src="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/visualizebutton.png" /></a>

## Azure CLI command to deploy IoT Edge enabled VM

```bash
az group deployment create \
  --name edgeVm \
  --resource-group replace-with-rg-name \
  --template-uri "https://aka.ms/iotedge-vm-deploy" \
  --parameters dnsLabelPrefix='my-edge-vm1' \
  --parameters adminUsername='azureuser' \
  --parameters deviceConnectionString=$(az iot hub device-identity show-connection-string --device-id replace-with-device-name --hub-name replace-with-hub-name -o tsv) \
  --parameters authenticationType='sshPublicKey' \
  --parameters adminPasswordOrKey="$(< ~/.ssh/id_rsa.pub)"
```
