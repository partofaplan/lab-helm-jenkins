# lab-helm-jenkins

A simple repo for customizing the https://github.com/jenkinsci/helm-charts helm chart. This app can be deployed by using `helm upgrade --install myjenkins -f values.yaml jenkins/jenkins`.

##TODO
Need to embed the pipelines for deploying the weathervane app within the Jenkinsfile so when it's deployed the configuration contains the job.
