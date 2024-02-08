1. Create simple app
https://github.com/nova34tkj4/pintu-test.git
![image](https://github.com/nova34tkj4/pintu-test/assets/26535997/8eaf7e27-a0da-4395-899e-fa69970dc603)

2. Create CI/CD 
Deploy use Gitlab & Jenkins 

Gitlab 

![image](https://github.com/nova34tkj4/pintu-test/assets/26535997/bd708dfc-33b3-4816-82e1-dd640e7a3172)

Connect repositories from github
![image](https://github.com/nova34tkj4/pintu-test/assets/26535997/d1022c42-dcac-4e3a-a2e1-54afd4a50b3b)

ci/cd variables 
![image](https://github.com/nova34tkj4/pintu-test/assets/26535997/ae34f41c-6673-42aa-9080-c4157c132911)

Gitlab-ci.yml
<img width="551" alt="image" src="https://github.com/nova34tkj4/pintu-test/assets/26535997/299891c6-84e6-4d00-b360-af6421ab3511">

build Success 
![image](https://github.com/nova34tkj4/pintu-test/assets/26535997/e6930f88-a4a8-4e56-92ed-b83b3a32ce3d)


Jenkins

Pipeline Jenkins 

<img width="797" alt="image" src="https://github.com/nova34tkj4/pintu-test/assets/26535997/bcf82827-4d15-4752-9f17-203cb375c8a4">
Store container image to a registry
![image](https://github.com/nova34tkj4/pintu-test/assets/26535997/d65680d5-ad1a-4f60-adb4-8dd38a7dfc25)
Deploy to Kubernetes cluster
-	Create service with port 3000 and use type clusterip
-	Create deployment with strategy RollingUpdate
-	Set resource cpu & memory for request and limit
<img width="333" alt="image" src="https://github.com/nova34tkj4/pintu-test/assets/26535997/6ded0996-7f61-48d5-9008-d572bed8094c">


3.	Service can consumed from public
My cluster Kubernetes use EKS, I’m setup nginx ingress controller & create nlb to provide external access to multiple Kubernetes services in your Amazon EKS cluster ( https://repost.aws/knowledge-center/eks-access-kubernetes-services ) and for SSL use letsencrypt.

Create SSL : 
Use route 53 in aws for manage my domain, and generate key use this command :
sudo certbot certonly --manual --preferred-challenges=dns --email novahariyakusuma@gmail.com --server https://acme-v02.api.letsencrypt.org/directory --agree-tos -d “*.novahariya.org”

This will generate key and add key to txt record on route 53

Create cert as secret :
kubectl create secret generic tls-cert --from-file=tls.crt=namaserver.crt --from-file=tls.key=namakeyprivate.key


Create ingress :
-	Create ingress use nginx for ingresslassname
-	Use annotations from nginx configuration for secure your application
-	Use domain has been registered on route 53 and uses the SSL secret that was previously generated
-	Pointing to service with servicename and port number
<img width="338" alt="image" src="https://github.com/nova34tkj4/pintu-test/assets/26535997/a34ce162-47a8-4a28-82be-a5d353309971">
