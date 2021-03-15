


Now you need a service account referencing those credentials in your secret. 

The manifest is pretty simple:
```editor:append-lines-to-file
file: ~/registry-service-account.yaml
text: |
        apiVersion: v1
        kind: ServiceAccount
        metadata:
          name: registry-service-account
        secrets:
        - name: registry-registry-credentials
        imagePullSecrets:
        - name: registry-registry-credentials
```

Apply your new service account.
```execute-1
kubectl apply -f registry-service-account.yaml
``` 