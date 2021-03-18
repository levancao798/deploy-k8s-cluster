### all node:
bash /path/nodesetup.sh
### on master node:
`bash
vim /etc/kubernetes/master-init.yaml 
kubeadm init --config /etc/kubernetes/master-init.yaml --upload-certs
`
###### coppy from master to worker:
`bash
kubectl -n kube-public get configmap cluster-info -o jsonpath='{.data.kubeconfig}' > discovery.yaml 
scp discovery.yaml user@host:/etc/kubernetes
`
###### install CNI:
`bash
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
`
### on worker:
`bash
vim /etc/kubernetes/worker-init.yaml 
kubeadm join --config /etc/kubernetes/worker-init.yaml
`
