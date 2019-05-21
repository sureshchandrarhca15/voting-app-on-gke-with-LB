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

NAME     DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
db       1         1         1            1           22m
redis    1         1         1            1           22m
result   1         1         1            1           22m
vote     1         1         1            1           22m
worker   1         1         1            1           22m


$ kubectl get pod -n vote 

NAME                      READY   STATUS    RESTARTS   AGE
db-5b7b495f94-jvdcp       1/1     Running   0          23m
redis-747699bd7f-g4rm4    1/1     Running   0          23m
result-7f9b75dcb5-cc47m   1/1     Running   0          23m
vote-697fd946fb-9xczt     1/1     Running   0          23m
worker-57cc69b79-hj877    1/1     Running   0          23m


$ kubectl get svc -n vote

NAME     TYPE           CLUSTER-IP      EXTERNAL-IP    PORT(S)          AGE
db       ClusterIP      10.39.245.240   <none>         5432/TCP         23m
redis    ClusterIP      10.39.246.127   <none>         6379/TCP         23m
result   LoadBalancer   10.39.253.78    34.83.253.89   5001:31495/TCP   23m
vote     LoadBalancer   10.39.248.106   35.197.57.12   5000:30687/TCP   23m


Step 4: As you can see, your voting app is exposed on port 5000 and result app is exposed on 5001: 
So access the below URLs: \n

For Vote	: http://10.39.248.106:5000
For Result	: http://10.39.248.106:5001 


