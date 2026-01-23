Day 1
--------
Pre-requisites: 
- A running kubernetes cluster which you can access from Server/client using kubeconfig file
  You can run a Kubernetes cluster locally in your machine using Kind(Kubernetes in Docker) utility, follow the steps in the official documentation and spin up a cluster: https://kind.sigs.k8s.io/docs/user/quick-start/
- helm package manager installed on the server/client from where we will be accessing the cluster.
  Follow steps mentioned for helm utility installation as per your machine specifications: https://helm.sh/docs/intro/install/
  
For Installation, we can follow below simple steps which I have referenced from Official documentation of Headlamp.

1) first add the custom repo to your local helm repositories
   
**helm repo add headlamp https://kubernetes-sigs.github.io/headlamp/**

now you should be able to install headlamp via helm

**helm install my-headlamp headlamp/headlamp --namespace kube-system**
<img width="1206" height="313" alt="image" src="https://github.com/user-attachments/assets/500151f6-7b7d-4f9e-b945-71a45016ff37" />


2) you can verify the installation using using below commands
   
**helm ls -n kube-system**
<img width="1084" height="99" alt="image" src="https://github.com/user-attachments/assets/4c8438bf-742f-42f3-99b3-201d1dad02a1" />

**kubectl get all --namespace kube-system -l app.kubernetes.io/instance=my-headlamp**
<img width="818" height="220" alt="image" src="https://github.com/user-attachments/assets/959fc228-4a95-44ee-af96-45a865e5426b" />
You should be able to see all the resources created by the headlamp.

Now for quickly accessing the UI, we can use port-forwarding the service and access it using localhost in our browser

**kubectl port-forward -n kube-system service/my-headlamp 8080:80**

3) Keep the port forwarding enabled and access the URL http://localhost:8080/ in you local browser. You should see below page from headlamp UI.
<img width="1919" height="1003" alt="image" src="https://github.com/user-attachments/assets/74259e52-ae95-4279-9e70-97efeb492548" />

Once you have this page, congratulations!! you have successfully Installed Headlamp.

