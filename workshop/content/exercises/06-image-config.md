

Now you're all ready to start building images and pushing them to your registry. To create a manifest that builds containers off the application code on GitHub:

Applying your image config will enable automation to build your new image.
This build will take a few minutes and will be subsequently faster each time you run as it has a cache. 

- Change `spec.tag` to your registry address appending `/app` or a name of your choosing to hold your app.
- Change `spec.serviceAccount` to your service account's name.
- At `spec.source.git.url` is the source code being used to build the app.
- The `spec.source.git.revision` is the commit used to build, a change here is one way to trigger a new build!

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
              revision: 82cb521d636b282340378d80a6307a08e3d4a4c4


```

```execute-1
kubectl apply -f registry-image.yaml
``` 

You can see the GitHub URL, and that you're building off master. Also, you configured the desired image tag (including the registry) and included the service account and builders you created. Once you apply this manifest, it will begin building.


By running `kubectl get images` you should see the image created but not complete:
```execute-1
kubectl get images
```

You will see the image name only, like so:
```
NAME              LATESTIMAGE   READY
petclinic-image                 Unknown
```