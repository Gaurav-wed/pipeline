pipeline {
    agent any 
    
    parameters {
        booleanParam(name: 'BOOL_PARAM', defaultValue: false, description: 'Boolean parameter')
        choice(name: 'ENV', choices: ['QA', 'UAT'], description: 'Select the environment')
    }
    
    triggers {
        pollSCM '* * * * *'
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh '/home/gaurav/Devops/apache-maven-3.9.6/bin/mvn install'
            }
        }
        stage('Deployment') {
            steps {
                script {
                    if (params.BOOL_PARAM) {
                        if (env.ENV == 'QA') {
                            sh 'cp target/pipeline.war /home/gaurav/Devops/apache-tomcat-9.0.88/webapps'
                            echo "Deployment has been COMPLETED on QA!"
                        } else if (env.ENV == 'UAT') {
                            sh 'cp target/pipeline.war /home/gaurav/Devops/apache-tomcat-9.0.88/webapps'
                            echo "Deployment has been done on UAT!"
                        }
                    } else {
                        echo "Please try again!"
                    }
                }
            }
        }
    }
}
