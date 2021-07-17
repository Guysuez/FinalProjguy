# FinalProjguy
YAMLs of first 16 questions:
first, if you cloned this repo, cd inside the folder "First-16-Question".

1. Deploy nginx pod:

kubectl apply -f 01-nginx-pod-deploy.yml

2. Deploy message pod:

kubectl apply -f 02-message-pod.yml

3. create a namespace:

kubectl create -f 03-namespace.yml

4. to create a json file with a list of nodes into a file named "nodes-guy", type this command: 

kubectl get -o json nodes > ./04-tmp/nodes-guy

5/6. Create a service to expose message pod:

kubectl apply -f 05-06-service-messaging-service.yml

07. create a deployment hr-web-app:

kubectl apply -f 07-hr-web-app-deployment.yml



09. create a pod named temp-bus on a namespace named finance-guy:

kubectl apply -f 09-pod-temp-bus.yml

10. create persistent volume:

kubectl apply -f 10-persistent-volume.yml

11. create a pod with volume EmptyDir:

kubectl apply -f 11-Pod-with-Volume.yml

12. create a pod with a persistent volume attached:

kubectl apply -f 12-pv-1-attched-pod.yml

13. create deployment and record the update:

kubectl apply -f 13-Deploy-and-update.yml;

kubectl set image deployment/nginx-deploy nginx=nginx:1.17 --record

this will show the update in the "annotations" when describing the deployment.


Pod Design Questions:
1. Type the command for:
Get pods with label information

kubectl describe pods, 

2. Create 5 nginx pods in which two of them is labeled env=prod and three of them is labeled env=dev:

kubectl apply -f Answer-for-Pod-Design-Q2.yml
or write;
kubectl run "name" --image=nginx --labels env=prod (X2)
kubectl run "name" --image-nginx --labels env=dev (X3)

3. Verify all the pods are created with correct labels

kubectl describe deployment deploy-dev; kubectl describe deployment deploy-prod

4. Get the pods with label env=dev
kubectl get -l env=dev

5. Get the pods with label env=dev and also output the labels

kubectl get pods -l env=dev -L env

6. Get the pods with label env=prod

kubectl get pods -l env=prod 

7. Get the pods with label env=prod and also output the labels

kubectl get pods -l env=prod -L env

8. Get the pods with label env

kubectl get pods -l env

9. Get the pods with labels env=dev and env=prod

kubectl get pods -L env | egrep 'dev|prod'

10. Get the pods with labels env=dev and env=prod and output the labels as well

kubectl get pods -L env | egrep 'dev|prod'

11. Change the label for one of the pod to env=uat and list all the pods to verify

kubectl label --overwrite pods/"podname" env=uat

if you applied the yml given in answer 2, you must change the labels inside the yml and apply again! the yml file defines the desired state for the deployment and the pods will not change the label.

12. Remove the labels for the pods that we created now and verify all the labels are removed

to remove:

kubectl label pods -l env env-

to verify:

kubectl get pods -l env

if you applied the yml file given in answer 2, you must change the yml! it is a deployment with labels and the deployment will act upon the desired state defined by the yml. 


13. Let’s add the label app=nginx for all the pods and verify (using kubectl)

kubectl label --all app=nginx

to verify:

kubectl get pods -L app

14. Get all the nodes with labels (if using minikube you would get only master node)

kubectl get nodes --show-lables

15. Label the worker node nodeName=nginxnode

kubectl label node/"nodename" nodeName=nginxnode

verify:

kubectl get nodes --show-labels 


16. Create a Pod that will be deployed on the worker node with the label nodeName=nginxnode

kubectl apply -f Answer-for-Pod-design-Q16.yml

17. Verify the pod that it is scheduled with the node selector on the right node… fix it if it’s not behind scheduled.

kubectl get pod nginx -o wide 


18. Verify the pod nginx that we just created has this label

kubectl describe pod nginx | grep Node-Selectors


Deployments:

1. Create the deployment:



