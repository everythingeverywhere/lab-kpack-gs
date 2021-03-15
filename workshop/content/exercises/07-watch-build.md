

If you run a `kubectl get pods`, you'll see a pod created (with a series of init containers) to build the image.
```execute-1
kubectl get pods
```

Since it includes six different containers, it's hard to use `kubectl logs` because you have to know which container to specify at which stage. It's much easier to use `Octant` mentioned at the beginning. 

The pod that is created has a name that starts with `<image-name>-build`; so in this case, `petclinic-image-build` from `metadata.name` in `~/registry-image.yaml`.

In `Octant` go to Workloads > Pods > `petclinic-image-build` > Logs to see the logs from your image being built.

Once it's complete you can recheck the image with `kubectl get images`:
```execute-1
kubectl get images
```

Your output will be similar to:
```
NAME LATESTIMAGE                                                                                                        READY
petclinic-image   {{ registry_host }}/spring-petclinic@sha256:<sha hash>   True
```

You can now run `docker pull {{ registry_host }}/app` to download the completed image. Or you can create a Kubernetes manifest to run the image.

**As mentioned in the previous section on image configuration, the `spec.source.git.revision` is the commit used to build, try changing it to trigger a new build!**

To try, delete `~/registry-image.yaml`
```execute-1
rm ~/registry-image.yaml
```
Now, create your `~/registry-image.yaml` file with the new revision `spec.source.revision` is another commit on the main branch we are picking randomly.

```editor:append-lines-to-file
file: ~/registry-image.yaml
text: |  
        apiVersion: kpack.io/v1alpha1
        kind: Image
        metadata:
          name: petclinic-image
          namespace: default
        spec:
          tag: {{ registry_host }}/app
          serviceAccount: registry-service-account
          builder:
            name: my-builder
            kind: Builder
          source:
            git:
              url: https://github.com/spring-projects/spring-petclinic
              revision: e2fbc561309d03d92a0958f3cf59219b1fc0d985


```

To apply your changes to your cluster:
```execute-1
kubectl apply -f ~/registry-image.yaml
```