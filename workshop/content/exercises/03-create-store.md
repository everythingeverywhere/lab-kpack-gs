A store is a repository of [buildpacks](http://buildpacks.io/) packaged into [buildpackages](https://buildpacks.io/docs/buildpack-author-guide/package-a-buildpack/) that kpack uses to build images. 

>You can add more languages by including more buildpacks you create or from [Paketo Buildpacks](https://github.com/paketo-buildpacks) we have only included a few bellow.

Create your store of buildpacks.
`store.yaml`
```editor:append-lines-to-file
file: ~/store.yaml
text: |
        apiVersion: kpack.io/v1alpha1
        kind: ClusterStore
        metadata:
          name: default
        spec:
          sources:
          - image: gcr.io/paketo-buildpacks/java
          - image: gcr.io/paketo-buildpacks/paketo-buildpacks/native-image
          - image: gcr.io/paketo-buildpacks/graalvm
          - image: gcr.io/paketo-buildpacks/dotnet-core
          - image: gcr.io/paketo-buildpacks/java-azure
          - image: gcr.io/paketo-buildpacks/nodejs
          - image: gcr.io/paketo-buildpacks/go
          - image: gcr.io/paketo-buildpacks/php
          - image: gcr.io/paketo-buildpacks/nginx
          - image: gcr.io/paketo-buildpacks/ruby

  ```
  
The store will be referenced by a builder resource.
```execute-1
kubectl apply -f store.yaml 
```
