# :rocket: Week1 Challenge of 10weekcloudops - Static Website hosting

#### Description :

:small_orange_diamond: Host a static website on AWS or Azure or GCP and implement CICD 

:small_orange_diamond: Services used : Azure storage, Azure CDN, GitHub Actions.

## Architecture 

![image](https://github.com/jananitework/week1-10weekcloudops/assets/136428700/dc4053f7-981f-4345-9148-5b891b174774)


## 💡 1. Host a static website 

```
1.1. Create a resource group to organise the Azure resources we will be creating.
1.2. Create a storage account under the resource group.
1.3. Enable static website and upload the default and error html pages in $web container . Try to access the primary endpoint 
```

## 💡 2. Integrate with Azure CDN

```
2.1. Create a new CDN profile and associate CDN endpoint to the Storage account.
2.2. Once its created, try to access the Endpoint hostname (it might take some time for the changes to reflect)
```

## 💡 3. Map a Custom domain

```
3.1. DNS Registrar : Create your own domain by registering with some DNS registrar. Map your desired subdomain with the CDN Endpoint hostname obtained in previos step.
3.2. Custom Domain in Azure : Associate a custom domain for your CDN endpoint. 
3.3. SSL/TLS : To validate your domain, you can either add own certicates and upload it in Azure Key Vault or use can leverage Azures CDN managed certificates.
```

## 💡 4. CI/CD : Github actions to deploy static site to azure

```
4.1. Create a GitHub repo for storing the html files.
4.2. We need a Service principle with neccessary permissions for Github application to access Azure resources.
- az ad sp create-for-rbac --name "myML" --role contributor --scopes /subscriptions/<subscription-id>/resourceGroups/<group-name> --sdk-auth
4.2. Github Actions : By configuring GitHub Actions, we can automatically deploy our site to Azure from GitHub when dev make changes to source code.
4.3. Create a workflow yaml file under .github/workflows in your repository's root folder.
4.4. Update secrets needed for Github Actions workflow file.

- AZURE_CDN_NAME :The CDN endpoint name created in 2.2
- AZURE_CDN_PROFILENAME : The CDN profile created in 2.1
- AZURE_CDN_RESOURCEGROUP : Resource group name
- AZURE_CREDENTIALS : output of the json of step 4.2
- AZURE_STORAGE_CONNECTIONSTRING :	Connection string of the storage account

```
Sample change to check workflow

#### References :
- https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blob-static-website-how-to?tabs=azure-portal
- https://learn.microsoft.com/en-us/azure/storage/blobs/storage-custom-domain-name?tabs=azure-portal
