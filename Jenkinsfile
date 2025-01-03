// Jenkinsfile (Declarative Pipeline) 
pipeline{
    agent {
        // run on the AGENT-1 node
        node {
            label 'AGENT-1'
        }
    }
    // parameters section, this section is used to define the parameters that can be used in the pipeline
    // define the environment variables canbe accesed globally ,the following are additional to existing environment variables
    options {
        ansiColor('xterm')
        timeout(time: 1, unit: 'HOURS')
        disableConcurrentBuilds()
    }
    // we need to get version from the application for this we use pipeline, for this we will use pipeline utilities plugin
    // this can be used across pipeline
    environment {
        packageVersion = ''
    }
    //build stages
    
    stages {
        stage('Get Version') {
            steps {
                script {
                    def packageJSON = readJSON file: 'package.json' 
                    packageVersion = packageJSON.version
                    echo "application version is ${packageVersion}"
                }
            }
        }
        stage('Install dependencies') {
            steps {
                sh """
                   echo 'install dependencies'
                   npm install
                """
            }
        }
        stage('Build') {
            steps {
                sh """
                  ls -lart
                  zip -r catalogue.zip ./* -x ".git" -x "*.zip"
                ls -lart

                """
            }
        }
    }
    // post section
    post {
        always {
            echo 'This will always run irrespective of status of the pipeline'
            // you need to delete workspace after the build because we are using the same workspace for all the builds
            deleteDir()
        }
        failure {
            echo 'This will run only if the pipeline is failed, We use thsi for alerting the team' 
        }
        success {
            echo 'This will run only if the pipeline is successful'
        }
    }
}
