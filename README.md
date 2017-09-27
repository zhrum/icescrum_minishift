# Installing icescrum into minishift

## Create user and set policies and create project
```
oc login -u system:admin
```
```
oc adm policy add-scc-to-user anyuid -z default
```
```
oc create user icescrum
```
```
oc login -u icescrum
```
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
