BELOW IS THE STEPS FOR SETUP KUBERNETS with kubeadm
====================================================================
=> First run below commands for kubernet setup

		-> apt-get update && apt-get install -y apt-transport-https curl
		-> curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
		-> cat <<EOF >/etc/apt/sources.list.d/kubernetes.list
		   deb https://apt.kubernetes.io/ kubernetes-xenial main
		   EOF
		-> apt-get update
		-> apt-get install -y kubelet kubeadm kubectl
		-> apt-mark hold kubelet kubeadm kubectl
		-> systemctl daemon-reload
		-> systemctl restart kubelet

=> After kubernet setup, set the pod network ip, using below command
		-> kubeadm init --apiserver-advertise-address=192.168.3.143 --pod-network-cidr=10.97.0.0/16
		
=> After above command kubets suggest few commands to run, please run those before move into next command

=> setup Calico 
		-> kubectl apply -f https://docs.projectcalico.org/v3.1/getting-started/kubernetes/installation/hosted/rbac-kdd.yaml
		-> wget https://docs.projectcalico.org/v3.1/getting-started/kubernetes/installation/hosted/kubernetes-datastore/calico-networking/1.7/calico.yaml
	edit the pod n/w id to 10.97.0.0/16 (for edit "i", for save and queit "wq")
		-> kubectl apply -f calico.yaml
=> Finally Master Isolation
		-> kubectl taint nodes --all node-role.kubernetes.io/master-

=> Check the status of kubernet using below command
		-> service kubelet status

=> Check how many pods running, using below command
		-> kubectl get pods -n kube-system


Tutorial for kubernet
https://www.youtube.com/watch?v=F-p_7XaEC84&list=PL9ooVrP1hQOF907pPru97cKY9nKwOrDTP
Setup kubernetes with kubeadm using below link
https://kubernetes.io/docs/setup/independent/install-kubeadm/		

======================================================================
1) Pod
2) Service
3) Job
4) Deployment
5) Networks
