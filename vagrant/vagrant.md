# Kubernetes cluster provisoning using Vagrant

https://github.com/justmeandopensource/kubernetes/tree/master/vagrant-provisioning

- In vagrant file update node count=3
- In bootstrap.sh in the last update the below line
    - 172.16.16.103   kworker3.example.com    kworker3

- After provisoning ensure you update name server as 8.8.8.8 on all of the servers
- Execute following commands on the master server
  - mkdir -p $HOME/.kube
  - sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  - sudo chown $(id -u):$(id -g) $HOME/.kube/config
