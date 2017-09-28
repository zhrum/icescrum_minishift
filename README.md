# Installing icescrum into minishift
Since Icescrum is a brand-new tool, no article explains how to install it into openshift.
I am telling here what I have experienced with minishift.

## Create user and set policies and create project
Log into minishift as system administrater
```
oc login -u system:admin
```

```
oc adm policy add-role-to-user system:deployer icescrum
```
Create a new user
```
oc create user icescrum
```
Log as the new user
```
oc login -u icescrum
```
Create a new project
```
oc new-project icescrum
```



## Create icescrum's app
```
oc new-app icescrum/icescrum
```

## Create icescrum's service
Add to Project -> import YAML/JSON
```console
apiVersion: v1
kind: Service
metadata:
  labels:
    app: icescrum
  name: icescrumservice
  namespace: icescrum
spec:
  clusterIP: 172.30.141.71  
  ports:
  - port: 8080              
    protocol: TCP
    targetPort: 8080
  selector:
    app: icescrum
    deploymentconfig: icescrum
  type: ClusterIP
```

## Create icescrum's route
* Name : icescrumroute
* Hostname : 
* Path : 
* Service : icescrumservice 
## Create icescrum's volum and attach volume to deployment
Create volume
* Name : icescrumstorage
* Access Mode : Single User (RWO) 
* Size : 10M

Attche volume
* Mount Path : /root


## Create postgres' app
```
oc new-app -e DB_USER=admin -e DB_PASS=admin -e DB_NAME=icescrum --docker-image="sameersbn/postgresql"
```

## Create postgres' volume and attach volume to deployment
Create volume
* Name : postgrestorage
* Access Mode : Single User (RWO) 
* Size : 50M

Keep the existing volume1 but delete volume2, then attach the new persistent one
* Mount Path : /var/lib/postgresql

## Initial configuration
Go to the main page of icescrum : <icescrumroute>/icescrum
* Database:                   PostgreSQL
* URL:                        jdbc:postgresql://postgresql:5432/icescrum
* User:                       admin
* Password:                   admin

## Finally
Scale icescrum service to 0 pod then 1 pod.


