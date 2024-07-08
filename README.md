# centralized-logging-EFK

Step 1:
git clone https://github.com/Shubham2194/centralized-logging-EFK.git


cd centralized-logging-EFK && 
kubectl apply -f .

kubectl get all

![image](https://github.com/Shubham2194/centralized-logging-EFK/assets/83746560/ffe14aaa-8962-4c54-a737-a09beb8aac3f) 

Step 2:
Lets access the kibana dashboard with the added URL in ingress 
if you dont have ingress controller please configure it from here ( https://docs.nginx.com/nginx-ingress-controller/installation/installing-nic/installation-with-manifests/ )

![image](https://github.com/Shubham2194/centralized-logging-EFK/assets/83746560/bf937a3b-ded2-489e-b166-ef13aed1821b)



![image](https://github.com/Shubham2194/centralized-logging-EFK/assets/83746560/4ebcc192-328e-4b1f-8b2b-1ecbdd38c562)

Step 3:
Adding basic auth

sudo apt-get install apache2-utils

htpasswd -c auth kibanauser

kubectl create secret generic kibana-basic-auth --from-file=auth -n logging

Now add these annotations in ingress

    nginx.ingress.kubernetes.io/auth-type: "basic"
    nginx.ingress.kubernetes.io/auth-secret: "kibana-basic-auth"
    nginx.ingress.kubernetes.io/auth-realm: "Authentication Required"

![image](https://github.com/Shubham2194/centralized-logging-EFK/assets/83746560/bd0cc1b4-f4c2-49b6-a2a2-c1cbb46df1b8)



Step 4: 
Add index pattern to discover our Logs 

Follow : home > Stack management > index patterns


Select create index pattern

![image](https://github.com/Shubham2194/centralized-logging-EFK/assets/83746560/ae0f6d7a-d892-4344-ad54-6723ba2f3978)

Write : 
logstash-* and hit next step


![image](https://github.com/Shubham2194/centralized-logging-EFK/assets/83746560/65dd5a21-a29e-46af-ad77-3dd491fe3024)

We have successfully added or index 

Step 5:
Discover our logs

Move to home page and hit discover


Turn on KQL 

![image](https://github.com/Shubham2194/centralized-logging-EFK/assets/83746560/fdc58ddc-8e19-40f6-a0d3-95379ef684fd)


FETCH the Logs : 

search - kubernetes.container_name : backend


![image](https://github.com/Shubham2194/centralized-logging-EFK/assets/83746560/453249d5-7349-4ef1-a918-d387d2aeb2c0)

Happy Logging !!!
