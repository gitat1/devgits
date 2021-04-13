pipeline {
  
  agent any
  
  stages{
    stage("build") {
      steps {
        echo "Building application..."
      }
    }
    stage("test") {
      // if you want to run test only on specific env/ branch then can use when clause, now webhook enabled
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
        // you can now read credentials setup in jenkins and deploy this to server, i.e. for login
        withCredentials([
          usernamePassword(credentials: 'stringnamesetup in jenkins', usernameVariable: USER, passwordVariable: PWD)
        ]){
          // now you can use $USER  and $PWD to read the username and pwd and use in sh file
          sh "copy artifact, unzip file, login into database using above credential and run database deployment"
          // this can be done after installing Jenkins credential and credential binding pluggins
        }
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
