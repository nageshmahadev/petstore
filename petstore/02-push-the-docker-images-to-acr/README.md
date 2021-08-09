# 02 - Push the Docker Images to Azure Container Registy (Local Development Only)

__This guide is part of the [Azure Pet Store App Dev Reference Guide](../README.md)__

In this section, we'll push the Docker Images to Azure Container Registy

**1. Push the Pet Store App Docker Image to Azure Container Registry**

> 📝 Please Note, Since the Docker Images were built in the previous guide, we can run from any path on the terminal. But if you prefer, or if you plan to build more images, cd to azure-cloud/petstore/petstoreapp 

> 📝 Please Note, We will assume you have forked the azure-cloud repository, it is the easiest way to get going (for instructions on this view the "**Forking the azure-cloud**" section in [00-setup-your-environment](../00-setup-your-environment/README.md). Also, both PetStoreApp and PetStoreService use a Spring Boot Application properties file named application.yml to drive the functionality/configuration of these applications which is located in src/main/resources/application.yml of both projects. By default, this file has all of the properties that are needed throughout the guides, and by default are commented out. This means that the applications will start automatically without having to configure anything. As you progress through the guides, each guide will inform you of what properties to uncomment and configure within your environment. If you have not already done so, login to your GitHub account, head to https://github.com/chtrembl/azure-cloud, and fork.

run the following commands:

```az login``` 

```az account list --output table```

> 📝 Please Note, use your subscription for "your subscription" and your container registry value for "youraliaspetstorecr" from the first guide 00-setup-your-environment

```az account set --subscription <your subscription>```

```az acr login --name <youraliaspetstorecr>```

> 📝 Please Note, the following is what enables us to get Web Hook control for our App Service Continuous Integration

```az acr update -n <youraliaspetstorecr> -g <yourresourcegroup> --admin-enabled true```

> 📝 Please Note, tag your local Docker image built in the previous guide so that we can push it to Azure Container Registry then push it

```docker image tag petstoreapp:latest <youraliaspetstorecr>.azurecr.io/petstoreapp:latest```

```docker push <youraliaspetstorecr>.azurecr.io/petstoreapp:latest```

You should see something similar to the below image:

![](images/petstoreapp_push.png)

If you head to Azure Portal and view your Container Registry Resource "youraliaspetstorecr" you should see something similar to the below image:

![](images/petstoreapp_cr.png)

**1. Push the Pet Store Service Docker Image to Azure Container Registry**

> 📝 Please Note, Since the Docker Images were built in the previous guide, we can run from any path on the terminal. But if you prefer, or if you plan to build more images, cd to azure-cloud/petstore/petstoreservice

You are still logged in from before...

run the following commands:

> 📝 Please Note, tag your local Docker image built in the previous guide so that we can push it to Azure Container Registry then push it

```docker image tag <petstoreservice>:latest <youraliaspetstorecr>.azurecr.io/petstoreservice:latest```

```docker push <youraliaspetstorecr>.azurecr.io/petstoreservice:latest```

Things you can now do now with this guide

☑️ Administration of Azure Container Registry, pushing of Docker Images

---
➡️ Next guide: [03 - Configure App Service for continuous deployment](../03-configure-app-service-for-cd/README.md)
