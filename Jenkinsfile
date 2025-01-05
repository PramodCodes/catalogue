#!groovy
// this is a centralised pipeline for project which is running on nodejs server which we will parameterise 
// nodejsvm is a centralised vm which will be used by all the projects similarly we will have javavm/govm/pythonvm
@Library('roboshop-shared-library') _
// responsible to pass what type of appication and component is running in pipeline through pipeline decission file

def configMap = [
    appication: "nodejsVM",
    component: "catalogue"
]

env