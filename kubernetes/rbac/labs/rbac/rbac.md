### Objective

A sample application which will return permissions of Secrets are allowed.

### Relevant Material

[Tutorial]()

[Video]()

### Code Repository

https://github.com/CloudplexPlatform/k8s-rbac-sample-app

### Add RbacFet Service

RbacFet application is a restful microservice which will return **Rbac permissions** of the Kubernetes Secret object

Locate the **Container** services from K8 resources in the pallet.

![Lab05-container-service-configuration-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/rbac/labs/rbac/images/Lab05-container-service-configuration-01.png)

Drag-n-drop **container** service from pallet to canvas

![Lab05-container-service-configuration-02](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/rbac/labs/rbac/images/Lab05-container-service-configuration-02.png)

Select the service to open configuration of the service on the right side of the window

![Lab05-container-service-configuration-03](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/rbac/labs/rbac/images/Lab05-container-service-configuration-03.png)

1. Change name of the service to **rbacfet**

   ![Lab05-container-service-configuration-04](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/rbac/labs/rbac/images/Lab05-container-service-configuration-04.png)


2. Enter the image name **cloudplexng/rbacfet**

   ![Lab05-container-service-configuration-05](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/rbac/labs/rbac/images/Lab05-container-service-configuration-05.png)

4. Enter tag of the image **v1**

   ![Lab05-container-service-configuration-06](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/rbac/labs/rbac/images/Lab05-container-service-configuration-06.png)

#### Add new Port

[Ports](https://kubernetes.io/docs/concepts/services-networking/connect-applications-service/#the-kubernetes-model-for-connecting-containers) are required to access your applications. Click on the **Port section** to add a new port

![Lab05-container-service-configuration-07](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/rbac/labs/rbac/images/Lab05-container-service-configuration-07.png)

Click on Add ports button to add a new port

```yaml
name : http-3550
container Port : 3550
```
![Lab05-container-service-configuration-08](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/rbac/labs/rbac/images/Lab05-container-service-configuration-08.png)


#### Add RBAC permissions

[RBAC](https://kubernetes.io/docs/reference/access-authn-authz/rbac/) provide authroization and authentication access to resources

Click on the Advanced Configurations to open Advanced Configurations

![Lab05-rbac-options-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/rbac/labs/rbac/images/Lab05-rbac-options-01)

Select Rbac option to configure rbac rules

![Lab05-rbac-options-02](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/rbac/labs/rbac/images/Lab05-rbac-options-02)

Enable the rbac button 

![Lab05-rbac-options-03](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/rbac/labs/rbac/images/Lab05-rbac-options-03)

Click on Add resource based roles

```yaml
Resource: Secrets
Action: List 
```
![Lab05-rbac-options-04](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/rbac/labs/rbac/images/Lab5-rbac-options-04)


Click on the back button on top of the configurations.

![lab02-configure-service-21](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/deployment/labs/guestbook/images/lab02-configure-service-21.png)

### Enable Ingress Traffic

​[Ingress gateway](https://istio.io/docs/tasks/traffic-management/ingress/ingress-control/) will allow you to access service from the internet. Click on the Ingress section to enable ingress traffic.

![Lab05-container-service-configuration-09](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/rbac/labs/rbac/images/Lab05-container-service-configuration-09.png)

Click on the back button on top of the configurations.

##### Save Service

Click on the save button to save the configuration of the service

### Save Application

Click on the **Save** button at the bottom right corner

![Lab05-application-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/rbac/labs/rbac/images/Lab05-application-01.png)



### Your Application Logs

In the log window, you can see the logs of your infrastructure, Kubernetes Cluster and Application which you have deployed.

**!! Deployment will take around 15 minutes!!** 

![Lab05-Deployment-Logs-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/rbac/labs/rbac/images/Lab05-Deployment-Logs-01.png)



### Accessing Your Application

Click on the App to get Ingress gateway Endpoint

![Lab05-Ingress-Endpoint-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/kubernetes/rbac/labs/rbac/images/Lab05-Ingress-Endpoint-01.png)



Copy Ingress Endpoint and Paste in browser new Tab. 

Open Postman or any tool you preferred for APIs.

Create a new request to see the permissions on the resource.

```yaml
Request Type: GET
Request Endpoint: <Ingress IP>/permissions
```



### Cleanup

Click on the **Terminate** button to remove all the resources from the cloud.
