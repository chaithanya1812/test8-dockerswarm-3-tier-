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
