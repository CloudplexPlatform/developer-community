### Objective

This Lab will help you understand how to define RBAC policies for your Kubernetes Application.


### Prerequisite

If you want to deploy this lab, you need to deploy at least one infrastrture. We have labs on infrastrture as well, you can follow them to deploy infrastructure


### Add Application Info

Give name to your application and specify the version, you can also give tags to your application of your choice.

![app-info](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/rbac/labs/rbac/images/1.png)

Click on the **next** button on the top right corner.


CloudPlex has integrated with [Docker Hub](https://hub.docker.com/) registry which allows users to access prebuilt images. You can fetch images metadata (Environment variables, Ports).

Drag **Docker Hub** service from palette and drop it on canvas. 

![ezgif.com-video-to-gif](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/rbac/labs/rbac/images/2.gif)


### Search RBAC Service  

Click on the service to show search panel of the service from Docker Hub.

- Type **[cloudplexng/k8s-rbac](https://hub.docker.com/r/cloudplexng/k8s-rbac)**
- Select Community from the filter
- Now, click on the search button and select **Cloudplexng/K8s-Rbac** service.

![rbac-service-dockerhub](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/rbac/labs/rbac/images/3.png)

Cloudplex will fetch all the details and the latest tag of the image itself.


### Add new Port

[Ports](https:/kubernetes.io/docs/concepts/services-networking/connect-applications-service/#the-kubernetes-model-for-connecting-containers) are required to access your applications. Click on the **Port section** to add a new port

![Lab04-Add-Ports-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/rbac/labs/rbac/images/4.png)

Cloudplex automatically discovers ports from Docker images and populates them in the ports section of the service.

![Lab04-Add-Ports-02](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/rbac/labs/rbac/images/5.png)

Click on the back button on top of the configurations.

### Enable Ingress Traffic

​[Ingress gateway](https://istio.io/docs/tasks/traffic-management/ingress/ingress-control/) will allow you to access service from the internet. Click on the Ingress section to enable ingress traffic.

![Lab04-Ingress-traffic-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/rbac/labs/rbac/images/6.png)

Click on the back button on top of the configurations.


### Enable RBAC Configurations

Click on the ***Advance Configurations*** to enable RBAC and add Policies

[advance-configurations](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/rbac/labs/rbac/images/8.png)

Toggle the Enable RBAC button under the RBAC section.

![Enable-Rbac](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/rbac/labs/rbac/images/10.png)

CloudPlex supports  ***Role***, ***Role Binding***, ***Cluster Role***, and ***Cluster Role Binding***, see [Kubernetes RBAC](https://kubernetes.io/docs/reference/access-authn-authz/rbac/) to learn more about these.

For this lab, we are going to configure a ***Role*** and the rest of the configurations will be added automitically by Cloudplex.

Select an existing ***role*** available on the canvas from the dropdown, if you don’t have click on New.

![new-role](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/rbac/labs/rbac/images/11.png)

CloudPlex has populated default values of service (Service Id, Service Name, Namespace)

![pre-settings](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/rbac/labs/rbac/images/12.png)

Let’s add resources and actions. Click on the ***Add Resource Based Rules*** button

![add-resource-btn](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/rbac/labs/rbac/images/13.png)


Select ***Secrets*** from resource and ***GET*** and ***LIST*** from actions.

![rbac-conf](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/rbac/labs/rbac/images/18.png)

Click on ***Add API Groups*** button and add *.

![api-group](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/rbac/labs/rbac/images/19.png)

Cloudplex will create [Service Account](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#service-account-permissions) which will get attached to the running Kubernetes Pod to access the cluster resources.

Now Click on the ***Save*** button to save the role service.

![save-btn](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/rbac/labs/rbac/images/20.png)

Click again ***Save*** to save the main Dockerhub service that we dropped before.


### Deploy Application

Click on the **Deploy** button at the top right corner and select the ***infrastruture*** from the drop down list of your deployed infrastructures, your deployment will start right after saving the application and it will redirect you to the logs tabs or you can save it by clicking on the ***Save*** button to deploy it later.

![deploy-button](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/rbac/labs/rbac/images/13.png)


### Your Application Logs

In the log window, you can see the logs of your application.

**!! Deployment will take around 2 minutes!!** 

![Lab04-Deployment-Logs-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/rbac/labs/rbac/images/14.png)


### Accessing Your Application

Click on the Status tab to get Ingress gateway Endpoint
Copy Ingress Endpoint and Paste in browser new Tab.

Go to the following route.
```yaml
Ingress Endpoint/permissions

```

![app-access-endpoint](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/rbac/labs/rbac/images/ingress.png)


### Expected Result

You will get this screen by copying that ingress Endpoint in your browser

![Lab04-browser-output](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/rbac/labs/rbac/images/21.png)


### Cleanup

Click on the Terminate button to terminate your application and dont forget to Terminate the infrastrusture(s) that you used to deploy this lab.


### Conclusion

Congratulations! you just completed this lab and learned how to define RBAC poliy for your Kubernetes app using Cloudplex platform.


