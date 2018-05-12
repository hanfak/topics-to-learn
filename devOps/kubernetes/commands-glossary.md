
kubectl -n <namespace> <some action>
- generally need to refer to namespace to when runningcommands

kubectl describe  <pod name>

kubectl get pods

kubectl get jobs

kubectl logs  <pod name>
- get the logs

kubectl logs -f <pod name>
- Good for following the logs, as you use the app, and see the logs update as the app is processing the inputs/request

kubectl logs since=10 <pod name> > <file>
- Store logs up to some time, and store in file to browse and search later.

kubectl config use-context <CONTEXT_NAME>

kubectl delete pod  <pod name>
- if using helm, this will automatically bring up a new pod
