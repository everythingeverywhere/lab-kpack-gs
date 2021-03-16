Prereqs:
- kpack requires cluster admin permissions 
- Kubernetes 1.16+

To install:
Might need to login to sso, latest release from [here](https://github.com/pivotal/kpack/releases)
kubectl apply -f https://github.com/pivotal/kpack/releases/download/v0.2.2/release-0.2.2.yaml 

Ensure that the kpack controller & webhook have a status of Running using kubectl get.

kubectl get pods --namespace kpack --watch
---
For more detailed information on how to create and deploy workshops, consult
the documentation for eduk8s at:

* https://docs.eduk8s.io

If you already have the eduk8s operator installed and configured, to deploy
and view this sample workshop, run:

```
kubectl apply -f ./resources/workshop.yaml
kubectl apply -f ./resources/training-portal.yaml
```

This will deploy a training portal hosting just this workshop. To get the
URL for accessing the training portal run:

```
kubectl get trainingportal/lab-kpack
```

The training portal is configured to allow anonymous access. For your own
workshop content you should consider removing anonymous access.
