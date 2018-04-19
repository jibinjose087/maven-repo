#!groovy​
pipeline {
    agent any
        tools { 
            maven 'Maven 3.5.3' 
            }
        options {
        // Only keep the 10 most recent builds
        buildDiscarder(logRotator(numToKeepStr:'2'))
          }
        stages {
            stage ('Compile stage') {
                steps {
                sh  '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                    echo "compiled"                  
                    '''
                      }
                }
            stage ('package stage') {
                steps {
                  sh  '''
                        mkdir -p output                 
                        sh mvn clean compile
                       '''
                  writeFile file: "output/usefulfile.txt", text: "This file is useful, need to archive it."
                  writeFile file: "output/uselessfile.md", text: "This file is useless, no need to archive it."
                  }
                }
            stage ('archive stage') {
                steps {
                deleteDir()
            }
          }
          
          }
            post {
            
                always {
                    deleteDir()
                    echo 'I will always say Hello again!'
                    }
                success {
                    archiveArtifacts artifacts: 'output/*.txt', excludes: 'output/*.md'
            }
          }
    
  }

  
  
