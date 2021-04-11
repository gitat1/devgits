pipeline {
  
  agent any
  
  stages{
    stage("build") {
      steps {
        echo "Building application..."
      }
    }
    stage("test") {
      // if you want to run test only on specific env/ branch then can use when clause
      when {
        expression {
          echo "BRANCH_NAME is env variable that can be used, let say if want run test only on dev or master branch ...."
          BRANCH_NAME=="dev" || BRANCH_NAME=="master" // if this returns true then only next step will be executed... 
        }
      }
      steps {
        echo "Testing application..."
      }
    }
    stage("deploy") {
      steps {
        echo "Deploying application..."
      }
    }
  }
  post {
    always {
      // will be executed always irrespective whether build/ deploy succeeded or not
      echo "Send an email ..."
    }
    success {
      echo "Build is successful..."
    }
    failure {
      echo "Build is failed ..."
    }
  }
}
