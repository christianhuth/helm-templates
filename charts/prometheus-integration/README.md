# Scope

These examples don't show how to create a metrics endpoint in your application. It assumes that your Application already exposes metrics on a port called http-metrics, like this:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: <POD_NAME>
spec:
    containers:
    - name: <CONTAINER_NAME>
        image: <IMAGE_REGISTRY>/<IMAGE_REPOSITORY>:<IMAGE:TAG>
        ports:
        - name: http-metrics
            containerPort:
```
