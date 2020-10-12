#### Objective

In this lab, you will learn how to deploy a MySQL server using Cloudplex integrated Docker-Hub which will be used to pull pre-build MySQL image and use Persistent Volume to store data.

#### Prerequisite

If you want to deploy this lab, you need to deploy at least one infrastrture. We have labs on infrastrture as well, you can follow them to deploy infrastructure


#### Add Application Info

Give name to your application and specify the version, you can also give tags to your application of your choice.

![app-info](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/app-info.png)

Click on the **next** button on the top right corner.


#### Add Secret Service

CloudPlex platform provides a secret management service that provides the ability to store sensitive data such as passwords, tokens, and certificates in Cloudplex. Any data entered in this service is stored in a secure vault with at-rest encryption. This eventually becomes a [Kubernetes Secret](https:/kubernetes.io/docs/concepts/configuration/secret) in a deployed application.

To configure the service, Drag-n-drop **Secret service** from pallet to the canvas.

![secret-service](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/2.gif)

Click on the service to open the configuration panel on the right side.

The platform will populate the default values of service (Service Id, Service Name, Namespace)

![secret-service-info](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/3.png)

Click on Add secret string and type ***MYSQL_ROOT_PASSWORD*** in key and the Password in the value field. For this lab, type (the password as shown) ***5dzo2MsriVJNYTTtud8gOyDc3A*** in the value field.

![secret-key-password](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/4.png)

```yaml
key : MYSQL_ROOT_PASSWORD
value : 5dzo2MsriVJNYTTtud8gOyDc3A
```

Click on save button to save service

![button-save](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/5.png)


#### Configure the MySQL Container

Drag-n-drop the ***Docker Hub*** service from pallet to the canvas.

![docker-hub-service](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/6.gif)

Drag the arrow from ***Secret*** service to ***Container*** service.

![dockerhub-secret-link](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/7.gif)

Click on the service to open the configuration panel on the right side.

![docker-hub-service-configuration](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/8.png)

Type MySQL in the search bar and click on the search button.

![mysql-search](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/9.png)

Select MySQL service.

![mysql-service](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/10.png)

CloudPlex automatically pulls all the tags and metadata of the image and populates default values of service (Service Id, Service Name, Namespace, Type)


##### Add Environment Variables

Click on the **Environment variables section** to add a new [environment variable](https:/kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/#define-an-environment-variable-for-a-container).

Cloudplex provides two types of variables ([Static](https://docs.cloudplex.io/#/pages/user-guide/components/k8s-resources/container/container), [Dynamic](https://docs.cloudplex.io/#/pages/user-guide/components/k8s-resources/container/container)). We are going to use Dynamic variable in this lab to use the ***Secret*** key in our container

![dynamic-parameters](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/11.png)

Select the secret service from the service drop-down and type MYSQL_ROOT_PASSWORD in the key field.

![dynamic-variables-key](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/12.png)

Expand ***Service Attributes*** and Secrets Data and select ***MYSQL_ROOT_PASSWORD***. Cloudplex automatically generates dynamic  parameters for you.

![dynamic-variables-key-select](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/13.png)

Click on the save button to save the parameters.

![save-button-2](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/14.png)

A new environment variable with the key ***MYSQL_ROOT_PASSWORD*** will be added in the list of Environment Variables.

![saved-environment-variable](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/15.png)

Click on the back button on top of the configurations.


##### Add new Port

[Ports](https:/kubernetes.io/docs/concepts/services-networking/connect-applications-service/#the-kubernetes-model-for-connecting-containers) are required to access your applications. Click on the **Port section** to add a new port

![Add-Ports-01](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/16.png)

Cloudplex automatically discovers ports from Docker images and populates them in the ports section of the service.

![Add-Ports-02](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/17.png)

Click on the save button to save the service.

![service-save](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/18.png)


#### Add Volume Service

A [PersistentVolume](https:/kubernetes.io/docs/concepts/storage/persistent-volumes/) (PV) is a piece of storage in the cluster that has been dynamically provisioned by Kubernetes using a [StorageClass](https:/kubernetes.io/docs/concepts/storage/storage-classes).

MySQL service used this block of storage to store its data.

To add a persistent storage to your ***MySQL Service***, Click on the MySQL service to open the service configurations on the right side and click on  ***Advanced Configurations***

![container-service-advanced-configuration](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/19.png)

Select container volumes. CloudPlex has integrated with all the volumes and provides an easy to use interface for all of them.

![container-volumes](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/20.png)

For this lab, let's select persistent volume. Select Volume from service dropdown. If you don't have any volume available on canvas, you can create a new volume config by providing simple configurations.

Click on new from the service dropdown and CloudPlex will take you to the volume configurations panel.

![new-volume-service](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/21.png)

CloudPlex automatically populates default values of service (Service Id, Service Name, Namespace)

Enter desired capacity 10Gi and Reclaim policy Delete from dropdown. The reclaim policy for a PersistentVolume tells the cluster what to do with the volume after it has been released of its claim

![policy-and-capacity](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/22.png)

Click on the save button to save the configuration

![button-save](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/23.png)

Now you are back to your container service where you left it, Provide volume mount path. 

![mount-path](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/24.png)

Click on the save button to save the service.

![save-service](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/25.png)

All the Kubernetes manifest required to create a persistent volume (persistent volume claim, storageclass) is automatically created by the platform.

A [PersistentVolumeClaim](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) (PVC) is a request for storage by a user and a [StorageClass](https://kubernetes.io/docs/concepts/storage/storage-classes/) provides a way for administrators to describe the "classes" of storage they offer


#### Deploy Application

Click on the **Deploy** button at the top right corner and select the ***Infrastruture*** from the drop down list of your deployed infrastructures, your deployment will start right after saving the application and it will redirect you to the logs tabs or you can save it by clicking on the ***Save*** button to deploy it later.

In the log window, you can see the logs of your application.

![app-deployment-logs](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/26.png)

**!! Deployment will take around 2 minutes!!**

You can see the status of the application you just deployed by clicking on the app tab and click on Table view to see the realtime status of the services.

![app-status](https://raw.githubusercontent.com/CloudplexPlatform/developer-community/feature/github-data-fetching/applications/persistent%20volumes/labs/mysqlPv/images/28.png)


#### Cleanup

To avoid unnecessary costs, don’t forget to terminate your application when you are done.
Click on the Terminate button to terminate your application and dont forget to Terminate the infrastrusture(s) that you used to deploy this lab.


#### Conclusion

Congratulations! you just completed this lab and learned how to run a  ***My-SQL***  server with  ***Persistent Volume***  on Kubernetes using Cloudplex platform.


