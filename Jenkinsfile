#!groovy​
pipeline {
    agent any
        tools { 
        maven 'Maven 3.5.3' 
            }
        stages {
            stage ('Compile stage') {
                steps {
                sh  '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                    echo "compiled"
                    echo "JAVA_HOME = $JAVA_HOME"
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
            post {
            
                always {
                    deleteDir()
                    }
                success {
                    archiveArtifacts artifacts: 'output/*.txt', excludes: 'output/*.md'
            }
          }
    }
  }
