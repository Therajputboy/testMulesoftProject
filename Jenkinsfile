pipeline {
agent any
stages {
stage('Build Application') {
steps {
  bat 'mvn -B -U -e -V clean -DskipTests package'
}
}

 stage('Test') {
      steps {
          bat "mvn test"
      }
    }
    
stage('Deploy OnPremise Development') {
steps {
script{
  if(env.GIT_BRANCH == "origin/main")
  {
  	def env = "Development"
  	def target = "TPH-MULE-DEV"
  	def targetType = "server"
  }
  else if(env.GIT_BRANCH == "QA")
  {
  	def env = "qa"
  	def target = "TPH-MULE-UAT"
  	def targetType = "server"
  }
   else if(env.GIT_BRANCH == "Prod")
  {
  	def env = "Production"
  	def target = "TPH-MULE-PROD"
  	def targetType = "server"
  }
  else
  {
   echo "Branch not expected"
  }
}
echo 'Deploying mule project due to the latest code commit…'
echo 'Deploying to the configured environment….'
bat "mvn clean deploy -DmuleDeploy -DskipTests -Dmule.version=4.3.0 -Danypoint.username=rohit_tripointe -Danypoint.password=Tslplabap@123 -Dtarget=${target} -Dtarget.type=server -Denv=${env} -Dappname=cicd-test-app1"
}
}
}

post {
    failure {
        mail to: 'rohit.singh@apisero.com',
             subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
             body: "Something is wrong with ${env.BUILD_URL}"
    }
     success {
        mail to: 'rohit.singh@apisero.com',
             subject: "Successful Pipeline: ${currentBuild.fullDisplayName}",
             body: "Something is wrong with ${env.BUILD_URL}"
    }
}
}
