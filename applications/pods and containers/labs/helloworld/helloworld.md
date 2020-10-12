### Objective

This Lab will help you understand the concept of Pods and Containers by running a simple HelloWorld Application from CloudPlex.

### Code Repository

​https://github.com/cloudplex-io/hello-world


### Add Application Info

Give name to your application and specify the version, you can also give tags to your application of your choice.

![app-info](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/pods%20and%20containers/labs/helloworld/images/app-info.png)

Click on the **next** button on the top right corner.

### Add Service

CloudPlex has integrated with [Docker Hub](https://hub.docker.com/) registry which allows users to access prebuilt images. You can fetch images metadata (Environment variables, Ports).

Drag **Docker Hub** service from palette and drop it on canvas. 

![ezgif.com-video-to-gif](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/pods%20and%20containers/labs/helloworld/images/2.gif)



### Search Hello World Service

Click on the service to show search panel of the service from Docker Hub. 

- Type **[cloudplexng/helloworld](https://hub.docker.com/r/cloudplexng/helloworld)**
- Select Community from the filter
- Now, click on the search button and select **helloworld** service.



![helloworld-service-dockerhub](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/pods%20and%20containers/labs/helloworld/images/3.png)



CloudPlex will select the latest version of the image. 

![Lab01-Add-Tag](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/pods%20and%20containers/labs/helloworld/images/4.png)



### Add Environment Variables

They are required to  expose information to containers running in the Pod. Click on the **Environment variables section** to add a new [environment variable](https:/kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/#define-an-environment-variable-for-a-container).

![Lab01-Add-EnvironmentVariable-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/pods%20and%20containers/labs/helloworld/images/5.png)



CloudPlex provides two types of variables (**Static, Dynamic**). Let's add a static environment variable.

![Lab01-Add-EnvironmentVariable-02](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/pods%20and%20containers/labs/helloworld/images/6.png)

```bash
Key = PORT
Value = 3000
```

![Lab01-Add-EnvironmentVariable-03](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/pods%20and%20containers/labs/helloworld/images/7.png)

Click on the back button on top of the configurations.

### Add new Port

[Ports](https:/kubernetes.io/docs/concepts/services-networking/connect-applications-service/#the-kubernetes-model-for-connecting-containers) are required to access your applications. Click on the **Port section** to add a new port

![Lab01-Add-Ports-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/pods%20and%20containers/labs/helloworld/images/8.png)

Cloudplex automatically discovers ports from Docker images and populates them in the ports section of the service.

![Lab01-Add-Ports-02](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/pods%20and%20containers/labs/helloworld/images/9.png)

Click on the back button on top of the configurations.

### Enable Ingress Traffic

​[Ingress gateway](https://istio.io/docs/tasks/traffic-management/ingress/ingress-control/) will allow you to access service from the internet. Click on the Ingress section to enable ingress traffic.

![Lab01-Ingress-traffic-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/pods%20and%20containers/labs/helloworld/images/10.png)

Click on the back button on top of the configurations.

Click on the **Save** button at the bottom right corner  to save your service

![Lab01-save-service-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/pods%20and%20containers/labs/helloworld/images/11.png)


### Deploy Application

Click on the **Deploy** button at the top right corner and select the ***infrastruture*** from the drop down list of your deployed infrastructures, your deployment will start right after saving the application and it will redirect you to the logs tabs.

![deploy-button](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/pods%20and%20containers/labs/helloworld/images/13.png)

### Your Application Logs

In the log window, you can see the logs of your application.

**!! Deployment will take around 2 minutes!!** 

![Lab01-Deployment-Logs-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/pods%20and%20containers/labs/helloworld/images/14.png)



### Accessing Your Application

Click on the Status tab to get Ingress gateway Endpoint
Copy Ingress Endpoint and Paste in browser new Tab.


### Expected Result

You will get this screen by copying that ingress Endpoint in your browser

![Lab01-browser-output](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/pods%20and%20containers/labs/helloworld/images/17.png)



### Cleanup

Click on the Terminate button to terminate your application and dont forget to Terminate the infrastrusture(s) that you used to deploy this lab.

### Conclusion

Congratulations! you just completed this lab and learned how to deploy a Hello-World app on Kubernetes using Cloudplex platform.

