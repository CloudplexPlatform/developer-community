#### Objective

In this lab, you will learn how to create and use your own kubernetes cluster on AWS cloud.

#### Set up Basic Information

Cloudplex platform will populate the basic info (Infrastructure name, Infrastructure Id) itself.

For this lab, we will use [AWS](https://aws.amazon.com/) as our cloud provider (you must have an account on AWS in order to use it). Provide cloud provider credentials and save them as profile for future use.

![user-profile](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/infrastructures/user%20managed/labs/awsUserManaged/images/2.png)

Cloudplex platform provide an easy way to save all your [Secret Credentials](https://docs.cloudplex.io/#/pages/user-guide/components/credentials-profile/credentials-profile?id=credentials-profile) in a secure vault.

Select the region & zone where you want to create your cluster.

Click on the ***Next*** button.

![next-button](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/infrastructures/user%20managed/labs/awsUserManaged/images/21.png)


#### Configure AWS Network

CloudPlex automatically configures a complete network for you. 

One  [VPC](https://aws.amazon.com/vpc/), Two [subnets](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html), One [Security Group](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html), One Route Table, and One Internet Gateway are added and configured by the platform.

See [AWS](https://docs.aws.amazon.com/vpc/) documentation to further learn about these terms

![configured-network-subnets](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/infrastructures/user%20managed/labs/awsUserManaged/images/3.png)

![configred-security-group](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/infrastructures/user%20managed/labs/awsUserManaged/images/4.png)


#### Configure AWS cluster

Clicking on the ***next*** button will take you to the cluster tab.

![cluster-tab](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/infrastructures/user%20managed/labs/awsUserManaged/images/7.png)

CloudPlex will automatically create One [Node Pool](https://docs.cloudplex.io/#/pages/user-guide/components/cluster/um-new-cluster/aws-cluster/aws-cluster?id=aws) with default configurations. You may overwrite this with your own configuration.

![node-pool-configurations](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/infrastructures/user%20managed/labs/awsUserManaged/images/8.png)

Next you will select the Key type, if you have an existing ***SSH*** key, select it. If you want to generate a new key, provide the key name. 

![generate-key](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/infrastructures/user%20managed/labs/awsUserManaged/images/9.png)

Click on the ***generate*** button and it will save your generated key [credentials](https://docs.cloudplex.io/#/pages/user-guide/components/credentials-profile/credentials-profile?id=credentials-profile) in our secure vault.

![download-key](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/infrastructures/user%20managed/labs/awsUserManaged/images/15.png)

CloudPlex gives you an option to bring your own custom image or use market place Images

![container-image](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/infrastructures/user%20managed/labs/awsUserManaged/images/10.png)

Adding another node pool is easy, and you may do so by clicking on the Clone or Create button.

![add-another-pool](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/infrastructures/user%20managed/labs/awsUserManaged/images/11.png)

Now you have configured your cluster. Click on the ***Next*** button.

![next-kubernetes-conf](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/infrastructures/user%20managed/labs/awsUserManaged/images/12.png)

This is the Kubernetes configuration tab, where you can select your Kubernetes version and other options. For this lab, we will use the default configuration provided by the platform. 

![default-kuberntes-configuration](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/infrastructures/user%20managed/labs/awsUserManaged/images/13.png)

Click on the ***save*** button to save all your configurations.

![save-conf](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/infrastructures/user%20managed/labs/awsUserManaged/images/14.png)


##### provision your configured Infrastructure

Click on the Start button to start deploying your own Kubernetes cluster in the AWS cloud.

![start-button](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/infrastructures/user%20managed/labs/awsUserManaged/images/16.png)

You will see the logs as the infrastructure deployment progresses.

![deployment-logs](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/infrastructures/user%20managed/labs/awsUserManaged/images/17.png)

Click on the cluster tab to see the live status of your cluster.

![live-status-health](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/infrastructures/user%20managed/labs/awsUserManaged/images/18.png)

***Cluster live status*** is a complete dashboard that gives you the ***live status*** about the health and consumption of the nodes in your cluster

To avoid unnecessary costs, dont forget to terminate your infrastructure when you are done.

Click on the ***terminate*** button to delete all your resources from AWS.

![terminate-btn](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/infrastructures/user%20managed/labs/awsUserManaged/images/19.png)


#### Conclusion

You have just deployed a user-managed Kubernetes cluster on AWS using CloudPlex, the Kubernetes application platform for developers 
