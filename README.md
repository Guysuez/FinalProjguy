# FinalProjguy

1. assignment, deploying nginx pod:

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
