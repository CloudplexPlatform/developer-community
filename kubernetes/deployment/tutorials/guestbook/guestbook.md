### Objective

This is Guestbook Deployment Tutorial, which will help you to deploy Redis and Guestbook Application.

### Relevant Material

[Lab](https://learning.cloudplex.io/cloudplex-labs/docs/Lab2)

[Video]()

### Overview

In this tutorial, we’re going to discuss deployment. Once you've set up a cluster and built a container, the next step is to deploy. So how do you actually get your code up and running? Moreover, once your code is running, how do you update it (preferably without having to turn everything off and on). 

We’re going to go over configuring deployments, zero-downtime deployments, and how to roll back a bad deployment if you make a mistake. We’ll also discuss how these processes scale. It’s one thing to deploy a handful of replicas, but what complications arise when you’re deploying to hundreds or thousands?

### Basic Kubernetes Deployments
Deploying in Kubernetes is exceedingly simple. We’ve mentioned kubectl, the main Kubernetes command line tool, before. But here’s where it really starts to shine. We’ll be starting with two commands today: create deployment and get deployments.

Essentially, a deployment tells Kubernetes that a certain microservice needs to be running on a certain cluster. To create a deployment, you define a specification in  .yaml file. In the file, you’ll specify what you need for the deployment to happen: basic data such as the name and api version, as well as the nitty-gritty like which containers to deploy and how many.


```

controllers/sample-deployment.yaml

apiVersion: apps/v1

kind: Deployment

metadata:

  name: sample-deployment

  labels:

        app: sample

spec:

  replicas: 1

  selector:

        matchLabels:

          app: sample

  template:

        metadata:

          labels:

            app: sample

        spec:

          containers:

          - name: sample-container

            image: sample-container:1.0.0

            ports:

            - containerPort: 8000

```

After you've got the specification, you just need to use kubectl to create the deployment. The controller takes care of the rest. The specification is a declarative update. You describe what you want your deployment to look like (the services you run, how many instances, etc), and Kubernetes goes and makes it happen.

```

kubectl apply -f ./controllers/sample-deployment.yaml

```

Once you apply the deployment, you can see it in action. The get deployments command lists the state of all active deployments, so you can see what’s going on and where. Depending on the state of your changes, you’ll see the desired state you described in your specification as well as how close you are to achieving it.

```
kubectl get deployments
```

### Zero Downtime Deployments

Out of the box, Kuberenetes offers deployments with zero downtime. When you make an update to your service definition, say, by changing the container definition, Kubernetes will deployment using the “rolling update” strategy, which means it will replace old pods with new pods until the deployment is finished (there is an option to simply kill all the old pods and launch new ones, but it’s not as useful).

```
controllers/sample-deployment.yaml

template:

        metadata:

          labels:

            app: sample

        spec:

          containers:

          - name: sample-container

            image: sample-container:1.0.1

            ports:

            - containerPort: 8000

```

As above, you deploy the change by applying the new file to kubectl and you can check on the status by calling get deployments. You can see the rolling deployment kick in and evict old instances and replace them with new ones.

### Rolling Back

Sometimes in the course of a deployment, you realize the change breaks something important and you need to roll it back. Kubernetes keeps track of all the actions you take on a given deployment, which means rolling back is easy as well.

There are two forms of rolling back. First, if you’ve just done a deployment and need to roll back the latest changes you can use

```

kubectl rollout undo deployment.v1.apps/sample-deployment

```

And the latest deployment will be undone. Specifically, the deployment in progress will be stopped and the pods that received the new, bad code will be reverted to the old, good code.

The other option for rolling back is to specify the good version of the code to roll back to. This is similar to the above, but requires an additional parameter.

```

kubectl rollout undo deployment.v1.apps/sample-deployment --to-revision=2

```

Here, we know revision 2 is a good state, and we explicitly set the roll back to that version. This can be helpful if you’ve made multiple changes in succession.

### Scaling Concerns

A key concern in the Kubernetes world is how these practices scale when working with large services, or many services. In our original service definition above, we only included one instance (the replicas value). In a typical production deployment, you may want many more depending on your requirements.

Because the service definition included a starting value for replicas, we scale by modifying that value. Once we inform the kubectl controller of our desired change, it will make the requisite changes in our cluster. We can make that change in the command line

```

kubectl scale deployment.v1.apps/sample-deployment --replicas=10

```

And watch the deployment to see the replicas scale up to 10 instances.

