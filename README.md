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
 ##Nginx-server for  springboot-v:1.0
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
## OUTPUT of springboot-version-1.0
![deployv1ping1](https://user-images.githubusercontent.com/111736742/219812775-5fe8e7e1-a6ca-4b38-b614-0bcd98e58746.png)
## I make 3-enteries in springboot-v:1.0
## -------------------------------------------------------------
## Deploying springboot-v2.0
![dockerswarm4](https://user-images.githubusercontent.com/111736742/219813993-69518bee-af34-4f2e-877c-91f848b72841.jpg)
 ## Nginx-server Configuration file nginx.conf for  springboot-v:2.0
 #you need to modify this line proxy_pass http://chaitu; --------> proxy_pass http://chaitu1;
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
      proxy_pass http://chaitu1;
      }
  }

}
```
## Jenkins-dashboard to deploy springbootversion2.0
![deployversion2](https://user-images.githubusercontent.com/111736742/219812478-79cdb07c-5f4b-4a0e-af06-dcdd53c82930.png)
 ## Nginx-server for  springboot-v:2.0
 ![nginx-finalimg](https://user-images.githubusercontent.com/111736742/219812659-1fc43283-b1b5-44e1-a840-142e4fdc3651.png)
 ## ------------------------------------------------------------------------------------------------------------------------
 # Now to remove springboot-v:1.0 after your cureent version-v2.0 is stable.
 #Go To Docker manager node execute the following steps.
 ![toremoveservice](https://user-images.githubusercontent.com/111736742/219813407-56e6fda7-e292-490e-be21-179d3edc382d.png)

 


