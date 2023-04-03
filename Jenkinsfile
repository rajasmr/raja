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
                script {
                 def checkoutResult = checkout scm
                 checkoutResult[GIT]
                 env.GIT_BRANCH = checkoutResult["GIT"].toString().toLowerCase()
                 echo "This is your branch ${env.GIT_BRANCH}"
                }
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
