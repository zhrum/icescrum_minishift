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
## Import the YAML file to the project
* DB_USER : admin
* DB_PASS : admin

## Create icescrum's volum and attach volume to deployment
Create volume
* Name : icescrumstorage
* Access Mode : Single User (RWO) 
* Size : 10M

Attche volume
* Mount Path : /root

## Create postgres' volume and attach volume to deployment
Create volume
* Name : postgrestorage
* Access Mode : Single User (RWO) 
* Size : 50M

Scale postgressql to 0 pod.

Keep the existing volume1(/run/postgresql) but delete volume2(/var/lib/postgresql), then attach the new persistent one.
* Mount Path : /var/lib/postgresql

Scale postgressql to 1 pod.

## Initial configuration
Go to the main page of icescrum : \<icescrumroute\>/icescrum
* Database:                   PostgreSQL
* URL:                        jdbc:postgresql://postgresql:5432/icescrum
* User:                       admin
* Password:                   admin

## Finally
* Scale icescrum service to 0 pod.
* Scale postgre service to 0 pod.
* Scale postgre service to 1 pod.
* Scale icescrum service to 1 pod.

