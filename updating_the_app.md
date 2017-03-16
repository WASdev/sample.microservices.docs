### Updating the application

Once you've made some code changes, you'll want to redeploy the app. But `kubectl apply -f manifests` will say there's nothing to do unless the associated deployment yaml is modified. In a production setting this would occur by setting the specific version of the associated image. In our pipeline, we replace `imageName:latest` with `imageName:gitCommitId` to work around this. When testing locally you can add another label to spec.template.metadata.labels, or modify the value of an existing one. For example,

```
spec:
  replicas: 1
  template:
    metadata:
      labels:
        name: webapp-deployment
```

can become

```
spec:
  replicas: 1
  template:
    metadata:
      labels:
        name: webapp-deployment
        dummy: version1
```

and then next time,

```
spec:
  replicas: 1
  template:
    metadata:
      labels:
        name: webapp-deployment
        dummy: version2
```

There's a bug in kube where this will sometimes not work. Do please help us understand,
better work around, document, track and perhaps even fix this problem.
