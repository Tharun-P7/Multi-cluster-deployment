# Multicluster Deployment of application using ArgoCD and GitOps

The steps to deploy applications onto multiple Kubernetes clusters with Hub-Spoke model at the same time using Argo CD:

- Multiple Kubernetes clusters. You can create them using tools like eksctl or kubeadm.
- An Argo CD server installed on one of the Kubernetes clusters (preferably hub cluster).
  
Steps:
1. Clone the repository https://github.com/Tharun-P7/Multi-cluster-deployment
2. Create 3 kubernetes clusters (1 Hub cluster, 2 Spoke clusters) and make the current context as Hub cluster

![1](https://github.com/user-attachments/assets/71f2fbba-c0e6-4763-bd07-db64bde5e3bc)

3. Install ArgoCD by creating ArgoCD namespace and install ArgoCD

4. Change the service of ArgoCD from ClusterIP to NodePort
   ![2](https://github.com/user-attachments/assets/fe15a5d7-2e05-4853-910c-9b8e88af0672)

5. Make sure to include the necessary configuration for each cluster, such as the destination cluster name and namespace (argocd).
6. View the deployment of ArgoCD and check for the ExternalIP and port by ```kubectl get nodes -o wide``` and ```kubectl get svc -n argocd```
   
7. Login to the ```http://<ExternalIP>:<PortNo>```

 ![3](https://github.com/user-attachments/assets/a4c1e5b5-57ad-476f-bf6e-126cc206d09f)
8. Add both the spoke clusters to the hub cluster

![4](https://github.com/user-attachments/assets/c24ac08a-82c1-4928-8c0e-9473cd01faa3)

![5](https://github.com/user-attachments/assets/422d7f06-7bc8-462d-b9bd-e1430dbd371f)

9. Login to the UI and add all the necessary configurations and first add the spoke-cluster-1 and then spoke-cluster-2 individually
10. Create an application in Argo CD for each cluster you want to deploy to. Specify the destination cluster name and namespace in the application configuration.
11. Configure Argo CD to point to your Git repository and the application manifests.
12. Sync the applications in Argo CD. This will deploy your applications to the specified clusters.

    
![6](https://github.com/user-attachments/assets/a297a9f3-e025-4ccf-8e1f-5dc18c786f3b)

13. Now you can verify the changes deployed by changing any configuration by logging into the kubernetes cluster and you can see ArgoCD revokes the changes

Additional notes:

You can use Argo CD's auto-sync feature to automatically deploy changes to your applications as they are made to your Git repository.
You can use Argo CD's application sets feature to deploy the same application to multiple clusters with different configurations.
You can use Argo CD's rollback feature to roll back changes to your applications if something goes wrong.
