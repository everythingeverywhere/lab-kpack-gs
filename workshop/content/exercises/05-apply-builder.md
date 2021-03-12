
### Apply a Builder

A builder is an image that bundles all the bits and information on how to build your apps, like 
- A buildpack
- An implementation of the lifecycle
- A build-time environment that platforms may use to execute the lifecycle.

Kpack will push the builder image to your registry.

`builder.yaml`
- Change `spec.serviceAccount` to your service account's name.
- Change `spec.tag` to your registry address appending `/builder` or a name of your choosing to hold your builder.


```editor:append-lines-to-file
file: ~/builder.yaml
text: |
        apiVersion: kpack.io/v1alpha1
        kind: Builder
        metadata:
        name: my-builder
        namespace: default
        spec:
        serviceAccount: dockerhub-registry-service-account
        tag: {{ registry_host }}/builder
        stack:
            name: base
            kind: ClusterStack
        store:
            name: default
            kind: ClusterStore
        order:
        - group:
            - id: paketo-buildpacks/java
        - group:
            - id: paketo-buildpacks/java-azure
        - group:
            - id: paketo-buildpacks/graalvm
        - group:
            - id: paketo-buildpacks/nodejs
        - group:
            - id: paketo-buildpacks/dotnet-core
        - group:
            - id: paketo-buildpacks/go
        - group:
            - id: paketo-buildpacks/php
        - group:
            - id: paketo-buildpacks/nginx
```

```execute-1
kubectl apply -f builder.yaml 
```