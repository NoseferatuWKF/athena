az login without browser
```bash
az login --tenant <id> --use-device-code
```

managing cli
```bash
az upgrade
az extension add --name <name> --upgrade --allow-preview true
az provider register --namespace <namespace>
```

az extensions
```bash
# check for available commands
az --help
# check extensions
az extension list-available --output table
# if the command above fail do this
export REQUESTS_CA_BUNDLE=/path/to/cert.pem
# add extension
az extension add --name <extension>
# extensions are installed under ~/.azure
```

azure sql server via ssh tunnel
```bash
# set up port forwarding
ssh -Nf -L <host>:<port>:<remote>:<port> -i ~/.ssh/ssh.pem <user>@<remote>
# connect to db, example using sqlcmd
sqlcmd -S <host>,<port> -U <db-user>@<remote> -P <password> -d <database>
```

[ADO pipeline predefined variables](https://learn.microsoft.com/en-us/azure/devops/pipelines/build/variables?view=azure-devops&tabs=yaml)

acr
```bash
# login to azure cli
az login
# login to acr
az acr login -n <registry>
# if docker not installed or want to use the token directly
az acr login -n <registry> --expose-token
docker login <login-server> -u 00000000-0000-0000-0000-000000000000 -p <token>
# pull image
docker pull <registry>.azurecr.io/<image>:<tag>
```

container app
```bash
# create env
az containerapp env create --name $ENVIRONMENT --resource-group $RESOURCE_GROUP --location $LOCATION --output none
# create registry
az acr create --resource-group $RESOURCE_GROUP --name $REGISTRY_NAME --sku Basic --output none
# build image
az acr build -t $REGISTRY_NAME".azurecr.io/$CONTAINER_APP_NAME:$IMAGE_TAG" -r $REGISTRY_NAME /path/to/Dockerfile
# create container app
az containerapp create --name $CONTAINER_APP_NAME --resource-group $RESOURCE_GROUP --environment $ENVIRONMENT --image $REGISTRY_NAME".azurecr.io/$CONTAINER_APP_NAME:$IMAGE_TAG" --target-port 8080 --ingress external --registry-server $REGISTRY_NAME.azurecr.io
# update container app revision
az containerapp revision copy --name $CONTAINER_APP_NAME --resource-group $RESOURCE_GROUP --image "$REGISTRY_NAME.azurecr.io/$CONTAINER_APP_NAME:$IMAGE_TAG" --output none
# view container app
az containerapp show --name $CONTAINER_APP_NAME --resource-group $RESOURCE_GROUP
```

# bicep

[resources](https://learn.microsoft.com/en-us/azure/templates/)

general commands
```bash
# install bicep
az bicep install
# build to stdout
az bicep build --file /path/to/.bicep --stdout
# decompile ARM to bicep
az bicep decompile --file /path/to/.json
# generate params from bicep
az bicep generate-params --file /path/to/.bicep --output-format bicepparam --include-params all
```

deployment
```bash
# login to azure account
az login --tenant <tenant-id> --use-device-code
# check changes to subscription group before deployment
az deployment sub what-if --resource-group PskAIInitiative --template-file main.bicep
# deploy resource group to subscription
az deployment sub create --location <location> --template-file /path/to/.bicep
# check changes to resource group before deployment
az deployment group what-if --resource-group PskAIInitiative --template-file main.bicep
# deploy resource to resource group
az deployment group create --resource-group <resource-group-name> --template-file /path/to/.bicep
# check deployment history
az deployment operation group list --resource-group <resource-group-name> --name <deployment-name>
# get output value after deployment
az deployment group show --resource-group <your-resource-group> --name <your-deployment-name> --query properties.outputs.myOutput.value
# deploy via zip deploy endpoint
curl -X POST -u <user> --data-binary @<zipfile> https://{your-sitename}.scm.azurewebsites.net/api/zipdeploy
# deploy zip via cli
az webapp deploy --resource-group <group-name> --name <app-name> --src-path <zip-package-path>
```

[functions](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/bicep-functions)
