

If you run a `kubectl get pods`, you'll see a pod created (with a series of init containers) to build the image.
```execute-1
kubectl get pods
```

Since it includes six different containers, it's hard to use `kubectl logs` because you have to know which container to specify at which stage. It's much easier to use the `Octant` mentioned at the beginning. 

The pod that is created has a name that starts with `<image-name>-build`; so in this case, `petclinic-image-build` from `metadata.name` in `~/registry-image.yaml`.

In `Octant` go to Workloads > Pods > 

Once it's complete you can recheck the image with `kubectl get images`:

```
NAME LATESTIMAGE                                                                                                        READY
petclinic-image   {{ registry_host }}/spring-petclinic@sha256:<sha hash>   True
```

You can now run `docker pull {{ registry_host }}/<spring-petclinic>` to download the completed image. Or you can create a Kubernetes manifest to run the image.

**As mentioned in the previous section on image configuration, the `spec.source.git.revision` is the commit used to build, try changing it to trigger a new build!**
