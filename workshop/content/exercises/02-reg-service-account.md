


Now you need a service account referencing those credentials in your secret. 

The manifest is pretty simple:
```editor:append-lines-to-file
file: ~/dockerhub-service-account.yaml
text: |
        apiVersion: v1
        kind: ServiceAccount
        metadata:
        name: dockerhub-service-account
        secrets:
        - name: dockerhub-registry-credentials
        imagePullSecrets:
        - name: dockerhub-registry-credentials
```

Apply your new service account.
```execute-1
kubectl apply -f dockerhub-service-account.yaml
``` 