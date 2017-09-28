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

## Create icescrum's serviceapiVersion: v1

kind: Service
metadata:
  labels:
    app: icescrum
  name: serviceicescrum
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

## Create icescrum's route
## Create icescrum's volum
* Mount Path : /root


## Create postgres' app
```
oc new-app -e POSTGRESQL_USER=admin -e POSTGRESQL_PASSWORD=admin -e POSTGRESQL_DATABASE=icescrum --docker-image="registry.access.redhat.com/openshift3/postgresql-92-rhel7"
```

## Create postgres' volum

## Initial configuration
* Database:                   PostgreSQL
* URL:                        jdbc:postgresql://postgresql-92-rhel7:5432/icescrum
* User:                       admin
* Password:                   admin


