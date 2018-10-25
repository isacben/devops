<h1>Kubernetes Notes</h1>

References:

- https://kubernetes.io/docs/setup/minikube/

<h2>Minikube</h2>

Start minikube without vm (not recommended):

<pre>sudo /usr/local/bin/minikube start --vm-driver=none CHANGE_MINIKUBE_NONE_USER=true</pre>

Start minikube on virtualbox:

<pre>sudo /usr/local/bin/minikube start --vm-driver=virtualbox</pre>

Check minikube ip:
<pre>
  minikube ip
  192.168.1.27
</pre>

<h2>kubectl adjustments</h2>

To be able to run with current user (not root), you need to create an admin.conf file with permissions:

<pre>
sudo cp /etc/kubernetes/admin.conf $HOME/
sudo chown $(id -u):$(id -g) $HOME/admin.conf
export KUBECONFIG=$HOME/admin.conf
</pre>
