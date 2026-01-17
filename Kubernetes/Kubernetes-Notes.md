# Commands

- To get kubernetes component status - `kubectl get componentstatus`
- To get kubernetes nodes status - `kubectl get nodes`
- To get cluster info - `kubectl cluster-info`
- To get cluster version - `kubectl version` or `kubectl version --short`
- To create nginx pod - `kubectl create deploy nginx --image nginx`
- To expose the pod - `kubectl expose deploy nginx --port 80 --type NodePort`
