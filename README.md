## 3-Tier Application by Docker-swarm
#Deploying 3-Tier Java Application of two versions.

1.)springboot --> v:1.0 this version deployed in [dev-environment] called blue-environment.---------->accessing by the end-users.

2.)springboot --> v:2.0 this version is deployed in [qa-environment] called green-environment.--------->accessing by the qa-users, later getting all approvals
    from developers,testers and client this version is acessed by end users...
    
3.) By simply shifting load balancer to this version.    
    
## BLUE-GREEN DEPLOYMENT MODEL
![IMAGECHROME](https://user-images.githubusercontent.com/111736742/219729417-88639941-4e17-4122-9593-ecf011556201.jpg)
## -------------------------------------------------------------
## Blue-environment
1.Deploying 3-Tier Java Application of two versions.

2.springboot --> v:1.0 this version is accessing by the end-users first.
## Image
![docker-swarm2](https://user-images.githubusercontent.com/111736742/219730684-a0ebcd22-9420-472f-b8d9-c92c43a7a467.jpg)
## -------------------------------------------------------------------
## Building springboot-v:1.0
![depv1](https://user-images.githubusercontent.com/111736742/219800202-706f6b25-30fc-46d3-8ed9-8ba29ea339ba.png)
## Jenkins Dashboard version1
![version1dev](https://user-images.githubusercontent.com/111736742/219800658-bf70512d-a533-40a3-b875-4c1007bfa00e.png)
![deployver1](https://user-images.githubusercontent.com/111736742/219803669-e12b77b4-4a3a-4255-b203-8474855c4ef8.png)
## ##Nginx-server for  springboot-v:1.0
```bash
  events {}
http {
upstream chaitu{
server 13.232.1.17:8081;
server 15.207.111.244:8081;
server 3.110.122.170:8081;
}
upstream chaitu1{
server 13.232.1.17:8082;
server 15.207.111.244:8082;
server 3.110.122.170:8082;
}


server {
        listen 9000;
      location / {
      proxy_pass http://chaitu;
      }
  }

}
``` 
