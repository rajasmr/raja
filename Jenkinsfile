pipeline {

    agent any
    
    tools { 
        maven 'maven' 
    }

    options {
        buildDiscarder logRotator( 
                    daysToKeepStr: '15', 
                    numToKeepStr: '10'
            )
    }

    environment {
        APP_NAME = "DCUBE_APP"
        APP_ENV  = "DEV"
    }

    stages {
        
        stage('Cleanup Workspace') {
            steps {
                cleanWs()
                sh """
                echo "Cleaned Up Workspace for ${APP_NAME}"
                """
            }
        }
        
         stage('Checkout') {
            steps {
                 def checkoutResult = checkout scm
                 env.GIT_BRANCH = checkoutResult["GIT_BRANCH"].toString().toLowerCase()
                 echo ${env.GIT_BRANCH}
            }
        }


       
        
         stage('Code Build') {
            steps {
                 sh 'mvn clean install'
            }
        }

        stage('Priting All Global Variables') {
            steps {
                sh """
                env
                """
            }
        }

    }   
}
