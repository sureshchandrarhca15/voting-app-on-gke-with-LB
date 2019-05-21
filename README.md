############## The Voting App ##############

This is a simple application based on micro-services architecture, consisting of 5 simple services.

1. Voting-App: Frontend of the application written in Python, used by users to cast their votes.
2. Redis: In-memory database, used as intermediate storage.
3. Worker: .Net service, used to fetch votes from Redis and store in Postgres database.
4. DB: PostgreSQL database, used as database.
5. Result-App: Frontend of the application written in Node.js, displays the voting results.

Step 1: Use the below command to clone the Repository and cd into the voting app Spec folder: 

$ git clone https://github.com/sureshchandrarhca15/voting-app-on-gke-with-LB.git

$ cd voting-app-on-gke-with-LB/

Step2 2: The folder “k8s-specifications” contains the Kubernetes yaml specifications of the Voting App’s services. 
For each service it has two yaml files: a service file and a deployment file. 

$ ls  -l k8s-specifications/

Step 3: Time to create the service and deployment objects — piece of cake. 

Create a vote Namespace:

$ kubectl create namespace vote

Verify the Namespace:

$ kubectl get namespace

Create App's Deployments and and its Services: 

$ kubectl create -f k8s-specifications/

Verify the Deployments, Pods, and Services: 

$ kubectl get deployments -n vote 

$ kubectl get pod -n vote 

$ kubectl get svc -n vote


Step 4: As you can see, your voting app is exposed on port 5000 and result app is exposed on 5001: 
So access the below URLs: 

For Vote	: http://LoadBalancer_IP:5000
For Result	: http://LoadBalancer_IP:5001 


