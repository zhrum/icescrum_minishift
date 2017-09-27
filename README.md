# Installing icescrum into minishift

## Create user and set policies and create project
Log into minishift as system administrater
```
oc login -u system:admin
```

```
oc adm policy add-scc-to-user anyuid -z default
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

## Create icescrum's service
## Create icescrum's route
## Create icescrum's volum

## Create postgres' app
## Create postgres' volum

## Initial config
