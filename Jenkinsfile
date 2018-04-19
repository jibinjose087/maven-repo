pipeline {

  agent {
  
  }
  
  tools {
    jdk "jdk8"
    maven "mvn3.3.8"
  }
  
  environment {
    FOO = "BAR"
  }
  
  stages {
    stage("first stage") {
      steps {
          sh "mvn -version" 
        }
      }
      
      // Post can be used both on individual stages and for the entire build.
      post {
        success {
          echo "Only when we haven't failed running the first stage"
        }
        
        failure {
          echo "Only when we fail running the first stage."
        }
      }
    }
    
    stage('second stage') {
      tools {
        maven "mvn3.3.9"
      }
      
      steps {
        echo "This time, the Maven version should be 3.3.9"
        sh "mvn -version"
      }
    }
    
    stage('third stage') {
      steps {

        parallel(one: {
                  echo "I'm on the first branch!"
                 },
                 two: {
                   echo "I'm on the second branch!"
                 },
                 three: {
                   echo "I'm on the third branch!"
                   echo "But you probably guessed that already."
                 })
      }
    }
  }
  
  post {
    always {
      deleteDir()
    }
    
    success {
            echo "success"
    }

    failure {
            echo "failed"
    }
  }
  
  // The options directive is for configuration that applies to the whole job.
  options {
    // For example, we'd like to make sure we only keep 10 builds at a time, so
    // we don't fill up our storage!
    buildDiscarder(logRotator(numToKeepStr:'10'))
    
    // And we'd really like to be sure that this build doesn't hang forever, so
    // let's time it out after an hour.
    timeout(time: 60, unit: 'MINUTES')
  }

