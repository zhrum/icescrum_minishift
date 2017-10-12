# Installing icescrum into minishift
Since Icescrum is a brand-new tool, no article explains how to install it into openshift.

I have made a template file for minishift with postgresql.

Please note that it's necessary to create persistent volumes before starting the application, or pods scalings may break everything. 

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
## Import the YAML file to project
* DB_USER : admin
* DB_PASS : admin


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

