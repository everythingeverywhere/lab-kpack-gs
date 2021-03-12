

A [stack](https://buildpacks.io/docs/concepts/components/stack/) provides the buildpack lifecycle with build-time and run-time environments in the form of images.

The [pack CLI](https://github.com/buildpacks/pack) command: `pack suggest-stacks` will display a list of recommended stacks that can be used. We recommend starting with the `io.buildpacks.stacks.bionic` base stack. 

Now, create your stack.
`stack.yaml`
```editor:append-lines-to-file
file: ~/dockerhub-service-account.yaml
text: |
        apiVersion: kpack.io/v1alpha1
        kind: ClusterStack
        metadata:
        name: base
        spec:
        id: "io.buildpacks.stacks.bionic"
        buildImage:
            image: "paketobuildpacks/build:base-cnb"
        runImage:
            image: "paketobuildpacks/run:base-cnb"
```

Apply your stack
```execute-1
kubectl apply -f stack.yaml
```
