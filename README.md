# FinalProjguy
Final Project JB repo

1. assignment, deploying an nginx pod:

kubectl apply -f 01-nginx-pod-deploy.yml

2. Deploy message pod:

kubectl apply -f 02-message-pod.yml

3. create a namespace:

kubectl create -f 03-namespace

4. to create a json file with a list of nodes into a file named "nodes-yourname", type this command: 

kubectl get -o json nodes > ./04-tmp/nodes-guy

5. 