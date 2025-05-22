#argocd

****🚀 Argo CD Installation and Setup Guide****
This guide will help you install Argo CD on your Kubernetes cluster, expose the Argo CD server, and access its dashboard.

**Step 1: Create the argocd Namespace 📂**
Namespaces help isolate Argo CD resources from other workloads.

>>kubectl create namespace argocd

Verify the namespace:
>>kubectl get namespaces | grep argocd



Step 2: Install Argo CD in the argocd Namespace 📥
Apply the official Argo CD manifest:

>>kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

This deploys the API server, repo server, controller, and Dex for authentication.
________________________________________________________________________________________________________________________
sravan@sravankumar:~/AWS_DevOps/k8s/minikube/k8s/k8s-dep-yaml$ kubectl get namespace -n argocd

>>NAME              STATUS   AGE

>>argocd            Active   31h
________________________________________________________________________________________________________________________

Step 3: Service to NodePort🔌

>>kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'

Step 4: Retrieve Initial Admin Password 🔑
Get and decode the admin password:

>>kubectl get secrets -n argocd argocd-initial-admin-secret -o jsonpath='{.data.password}' | base64 -d && echo

#Port-Forwarding to 8081🔌
>>kubectl port-forward svc/argocd-server -n argocd 8080:443
________________________________________________________________________________________________________________________
**Port-forwarding...........**

sravan@sravankumar:~/AWS_DevOps/k8s/minikube/k8s/k8s-dep-yaml$ kubectl port-forward svc/argocd-server -n argocd 8081:443
Forwarding from 127.0.0.1:8081 -> 8080
Forwarding from [::1]:8081 -> 8080
Handling connection for 8081
Handling connection for 8081
________________________________________________________________________________________________________________________
**Additional Tips 💡**
Scale Argo CD Server for high availability:

>>kubectl scale deployment argocd-server -n argocd --replicas=2


![image](https://github.com/user-attachments/assets/a77d7a2c-7ea7-4343-8bce-c9797bba5302)

**Replica Count +1 added by sravankumar1006.**
![image](https://github.com/user-attachments/assets/066aa9c3-ef88-40e0-a849-7ab819058d37)


![image](https://github.com/user-attachments/assets/75eb338e-b9f6-4636-b1c9-41f5afd243bf)
