
# CI/CD Demo(PHP Application) with Tekton Pipelines

## Creating Openshift projects(CICD and APP_DEV)

    $ cicd_prj=cicd-app-php
    $ dev_prj=php-app-dev

    $ oc new-project $dev_prj
    $ oc new-project $cicd_prj
    

## Configure service account permissions for pipeline

    $ oc policy add-role-to-user edit system:serviceaccount:$cicd_prj:pipeline -n $dev_prj

    $ oc policy add-role-to-user system:image-puller system:serviceaccount:$stage_prj:pipeline -n $dev_prj
    

## Sonarqube Install and Configuration 

    $ oc create -f setup/sonarqube.yaml
    $ oc create configmap sonarconfig --from-file=config/sonar-project.properties
    

## Setup Tekton Pipelines

    $ oc create -f config/pipeline-pvc.yaml 

    $ oc apply -f task/sonarqube-scanner.yaml

    
