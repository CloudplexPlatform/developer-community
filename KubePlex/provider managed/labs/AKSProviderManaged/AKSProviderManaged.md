#### Objective

In this lab, you will learn how to create provider managed kubernetes cluster on azure.

#### Set up Basic Information

Provide cloud provider credentials and save them as profile for future use.(you must have an account on Azure in order to use it).

![user-profile](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/infrastructures/provider%20managed/labs/AKSProviderManaged/images/3.png)

Cloudplex platform provide an easy way to save all your [Secret Credentials](https://docs.cloudplex.io/#/pages/user-guide/components/credentials-profile/credentials-profile?id=credentials-profile) in a secure vault.

Select the region & zone where you want to create your cluster.

You can select either an existing resource group, if you have one; or create a new resource group. 

Click on the ***Next*** button.


#### Configure Network

CloudPlex automatically configures a complete network for you. But You can further customize your network based on your requirements.

![configured-network](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/infrastructures/provider%20managed/labs/AKSProviderManaged/images/4.png)

Clicking on the ***next*** button will take you to the cluster tab.

#### Configure AKS cluster

Cloudplex gives you three levels of configuration options, “simple”, “advanced”, and “expert”. 

In simple mode, CloudPlex requires machine type and number of nodes from the user and the rest of the configuration will be populated by the platform.

In advanced mode, you are able to customize your Kubernetes cluster including addition of multiple node pools, selection of Kubernetes version, and other features. Details vary from cloud to cloud.

In expert mode, you are also able to customize networking and other complex features. Details vary from cloud to cloud.

CloudPlex selects simple mode as the default option. We are using the default option for this Lab,

![default-kuberntes-configuration](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/infrastructures/provider%20managed/labs/AKSProviderManaged/images/5.png)


##### provision your configured Infrastructure

Click on the Start button to start deploying the infrastructure you have created on Azure.

![start-button](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/infrastructures/provider%20managed/labs/AKSProviderManaged/images/6.png)

You will see the logs as the infrastructure deployment progresses.

![deployment-logs](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/infrastructures/provider%20managed/labs/AKSProviderManaged/images/7.png)

Click on the cluster tab to see the live status of your cluster.


***Cluster live status*** is a complete dashboard that gives you the ***live status*** about the health and consumption of the nodes in your cluster

![live-status-health](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/infrastructures/provider%20managed/labs/AKSProviderManaged/images/8.png)

To avoid unnecessary costs, dont forget to terminate your infrastructure when you are done.

Click on the ***terminate*** button to delete all your resources from Azure.

![terminate-btn](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/infrastructures/provider%20managed/labs/AKSProviderManaged/images/9.png)


#### Conclusion

You just created a provider-managed Kubernetes cluster using CloudPlex, the Kubernetes Application Platform for Developers.


