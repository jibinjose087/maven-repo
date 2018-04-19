#!groovy​
pipeline {
    agent any
        options {
        // Only keep the 10 most recent builds
        buildDiscarder(logRotator(numToKeepStr:'2'))
          }

            stage ('test stage') {
                steps {
                echo "success"
            }
          }
            post {
            
                always {
                    deleteDir()
                    echo 'I will always say Hello again!'
                    }
                success {
                   echo 'I will always say success!' 
            }
          }
    }
