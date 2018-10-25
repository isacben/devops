<h1>Kubernetes Notes</h1>

References:

- https://kubernetes.io/docs/setup/minikube/

<h2>Minikube</h2>

Start minikube without vm (not recommended, don't do):

<pre>sudo /usr/local/bin/minikube start --vm-driver=none CHANGE_MINIKUBE_NONE_USER=true</pre>

Start minikube on virtualbox:

<pre>minikube start --vm-driver=virtualbox</pre>

Check minikube ip:
<pre>
  minikube ip
  192.168.1.27
</pre>

Create deployment (run is deprecated, check the command 'create':

<pre>kubectl run test-minikube --image=k8s.gcr.io/echoserver:1.10 --port=8080</pre>

Expose the deployment:

<pre>kubectl expose deployment test-minikube --type=NodePort</pre>

Check the pods:

<pre>kubectl get pod</pre>

<h2>kubectl adjustments</h2>

To be able to run with current user (not root), you need to create an admin.conf file with permissions:

<pre>
sudo cp /etc/kubernetes/admin.conf $HOME/
sudo chown $(id -u):$(id -g) $HOME/admin.conf
export KUBECONFIG=$HOME/admin.conf
</pre>
