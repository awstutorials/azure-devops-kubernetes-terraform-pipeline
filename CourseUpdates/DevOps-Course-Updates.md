# 148.Step 03 - Creating Azure DevOps Pipeline for Azure Kubernetes Cluster IAAC. 

**QUICK NOTE**

In the **subsequent step** of creating a Service Connection to Azure Resource Manager, please be aware that the user interface screens have been updated and may appear different.

**WHAT SHOULD YOU DO?**

Choose Azure Resource Manager as explained in the next video and choose options as shown below:

![How to create a new service connection](./images/azure-devops-new-azure-resourcemanager-serviceconnection.png)

1. Choose the option **Service Principle (Automatic)** and click **Next**

The next screen appears like this

![How to create a new service connection](./images/azure-devops-new-azure-resourcemanager-serviceconnection-02.png)

2. Choose the **azure subscription** from drop down

3. Leave the **Resource Group** Empty

4. Provide the service connection name as **azure-resource-manager-service-connection** 

5. Choose **Grand access permission to all pipelines** and click **Save**

# 152. Step 06 - Creating Azure DevOps Pipeline for Deploying Microservice to Azure AKS 1:30

**QUICK NOTE**

The upcoming step involves the creation of a service connection for Kubernetes.

However, due to an unresolved issue, the steps must be modified slightly.

**WHAT SHOULD YOU DO?**

In the **subsequent step** of creating a Service Connection to Azure Kubernetes, we need to use **KubeConfig** option instead of **Azure Subscription**

![How to create a new service connection](./images/azure-aks-connection.png)

**HOW TO GET KUBE CONFIG FOR AKS?**

1. Open your command prompt and execute the command **az login** .This will launch your browser and prompt you to select and log in to your desired account.

2. Run the command 

```
az aks get-credentials --name <name of the kubernetes cluster created> --resource-group <name of the resource group> --admin;
```

3. run cat ~/.kube/config; this command will show you config file details.
4. copy all content of files to your favourite text editor.
5. go to your service connection and choose KubeConfig from top radio button.
6. paste notepad's content in KubeConfig box.
7. choose cluster context <name of the cluster>
8. click on verify if its success then your job done. If you face any problems here, take a back up of the config file (~/.kube/config) and delete it. Run the command in step 2 again so that the config file contains only this kubernetes cluster.
9. Give connection name and click on last checkbox for permission.


 # 159. Step 01 - Review Terraform Configuration for AWS EKS Cluster Creation

AWS EKS has changed some of the configurations so we have udpated our repository with latest code.

1. The main.tf file now contains sections for creating EKS and then creating policy bindings after EKS is created. The sections which needs to be executed after the EKS creation are commented out now.
2. Follow the instructions given in the video to create the EKS cluster. There is no change in that.
3. Once the cluster is created, edit the main.tf and uncomment the sections marked as below

```
//>>Uncomment this section once EKS is created - Start
//>>Uncomment this section once EKS is created - End
```
and commit the file again. This will trigger the pipeline and policy bindings will be created.

4. Your final main.tf should look like the file final-main.txt in the same folder. You can compare your file with this one.