The first thing you need to do is tell `kpack` how to access the container registry to upload the completed images when they're done. 

You'll need a secret with credentials to access your container registry, so create the manifest `registry-credentials.yaml` and apply it with `kubectl apply -f`.

To create the `registry-credentials.yaml` manifest:

```editor:append-lines-to-file
file: ~/registry-credentials.yaml
text: |
        apiVersion: v1
        kind: Secret
        metadata:
          name: registry-credentials
          annotations:
            kpack.io/docker: {{ registry_host }}
        type: kubernetes.io/basic-auth
        stringData:
          .dockerconfigjson: {{ registry_auth_file}}

```

Apply your secret.
```execute-1
kubectl apply -f registry-credentials.yaml
```

