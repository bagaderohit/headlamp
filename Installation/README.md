Day 1
--------
Pre-requisites: 
- A running kubernetes cluster
- helm package manager installed on the server/client from where we will be accessing the cluster.
For Installation, we can follow below simple steps which I have referenced from Official documentation of Headlamp.

# first add the custom repo to your local helm repositories
helm repo add headlamp https://kubernetes-sigs.github.io/headlamp/

# now you should be able to install headlamp via helm
helm install my-headlamp headlamp/headlamp --namespace kube-system
<img width="1206" height="313" alt="image" src="https://github.com/user-attachments/assets/500151f6-7b7d-4f9e-b945-71a45016ff37" />


# you can verify the installation using using below commands
helm ls -A 
kubectl get all --namespace kube-system -l app.kubernetes.io/instance=my-headlamp

You should be able to see all the resources created by the headlamp




For Installing headlamp on your kubernetes cluster follow below process:
1) Clone the GitHub repository:
   $> git clone https://github.com/bagaderohit/headlamp.git

Once the repository is cloned go into the directory headlamp/installation/headlamp-0.39.0

2) Make sure that you have exported your cluster kubeconfig file and able to communicate successfully with clusterAPI.
   Execute the helm install command to install the chart into desired namespace. For example below I am installing headlamp in kube-system namespace with all the default values for the helmchart. We can ofcourse configure the values as per our need using the custom-values file or passing the values directly using --set parameter.
   $> helm install headlamp . -n kube-system 
