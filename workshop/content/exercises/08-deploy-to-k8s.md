Kpack is best used in conjunction with a CI/CD tool, but if you want to deploy your app to Kubernetes now you can very easily.

You will reuse your secret with your registry and pull from the repository that holds the container image.  You created this repo in the *Create an Image Configuration* section and can be found at  `spec.tag` place it after `--image=<registry>/<tag>` .

Create a deployment with the image kpack made with your source code
```execute-1
kubectl create deployment kpack-demo --image={{ registry_host }}/app   
```    

To verify deployment
```execute-1
kubectl get deployments                                          
```

Expose the Pod to the public internet using the kubectl expose command:
```execute-1
kubectl expose deployment kpack-demo --type=LoadBalancer --port=8080
```

The `--type=LoadBalancer` flag exposes your Service outside of the cluster.
The application code inside the image `k8s.gcr.io/echoserver` only listens on TCP port 8080.

To verify your service
```execute-1
kubectl get services                
```

On cloud providers that support load balancers, an external IP address would be provisioned to access the Service.
