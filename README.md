# edge-vm-deploy
ARM template to deploy a VM with IoT Edge pre-installed (via cloud-init)

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fveyalla%2Fedge-vm-deploy%2Fmaster%2FedgeDeploy.json" target="_blank">
    <img src="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.png"/>
</a>

The ARM template visualized for exploration
<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2Fveyalla%2Fedge-vm-deploy%2Fmaster%2FedgeDeploy.json" target="_blank"><img scr="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/visualizebutton.png" /></a>

## Azure CLI command to deploy IoT Edge enabled VM

```bash
# Create resource group
 az group create --name cig2 --location westus2

# Create VM, install IoT Edge and associate with IoT Hub device identity
az group deployment create \
  --name edgeVm \
  --resource-group cig2 \
  --template-uri "https://raw.githubusercontent.com/veyalla/edge-vm-deploy/master/edgeDeploy.json" \
  --parameters dnsLabelPrefix='testv1' \
  --parameters adminUsername='veyalla' \
  --parameters deviceConnectionString=$dcs \
  --parameters authenticationType='sshPublicKey' \
  --parameters adminPasswordOrKey="$(< ~/.ssh/id_rsa.pub)"
```
