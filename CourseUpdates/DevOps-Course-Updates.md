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

2. Run the command to get the credentials for AKS. This command automatically updates the config file in  **~/.kube/config**


**az aks get-credentials --name <name of the kubernetes cluster created> --resource-group <name of the resource group> --admin;**


3. Execute the command **cat ~/.kube/config**. This displays the content of the file.

4. Copy the entire content of file and paste it into your preferred text editor.

5. Proceed to your **service connection** and choose **KubeConfig** option from top radio button.

6. Paste the content from your text editor into the **KubeConfig** box.

7. Choose the appropriate cluster context 

8. Click on **verify** to check connection. 

> If any issues arise, create a backup of the config file (~/.kube/config) and delete the original. Then, repeat step 2 to ensure that the config file only contains information for this specific Kubernetes cluster.

9. Provide a connection name and check the last checkbox **Grant access permission for all pipelines** to enable permission for the pipelines to use this connection.


 # 159. Step 01 - Review Terraform Configuration for AWS EKS Cluster Creation

AWS EKS now needs a **TWO STEP process** to setup the cluster and create the policy bindings.

**GOOD NEWS:** The Course Repository has been updated to incorporate the necessary changes

Within the **main.tf** file, there are now designated sections to carry out the following actions:

1. Creating EKS Cluster

2. Establishing policy bindings following the creation of EKS.

**WHAT SHOULD YOU DO?**

Instead of a one step process, we would now need a two step process.

**STEP 1: CREATE CLUSTER**

NO CHANGE NEEDED!

Follow instructions in THE NEXT STEP AS-IS!

An EKS cluster should be created

**STEP 2: ESTABLISH POLICY BINDINGS**

1) After the cluster is created, edit **main.tf** - uncomment the sections marked as below:

> //>>Uncomment this section once EKS is created - Start

> //>>Uncomment this section once EKS is created - End

2) To initiate the pipeline and generate the policy bindings, **commit** the modified **main.tf** file to your GitHub repository. Ensure that the final version of your **main.tf** file matches the contents of the file final-main.txt. 

3) The provider kubernetes section should look like below

```
provider "kubernetes" {
  //>>Uncomment this section once EKS is created - Start
  host                   = data.aws_eks_cluster.cluster.endpoint #module.in28minutes-cluster.cluster_endpoint
  cluster_ca_certificate = base64decode(data.aws_eks_cluster.cluster.certificate_authority[0].data)
  token                  = data.aws_eks_cluster_auth.cluster.token
  //>>Uncomment this section once EKS is created - End
}
```
