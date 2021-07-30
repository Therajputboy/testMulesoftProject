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
    
stage('Deploy OnPremise') {
steps {
script{
  if(env.GIT_BRANCH == "Dev")
  {
    
    echo 'Deploying mule project due to the latest code commits in Dev branch…'
    echo 'Deploying to the Development environment….'
    /*bat 'mvn clean deploy -DmuleDeploy -DskipTests -Dmule.version=4.3.0 -Danypoint.username=rohit_tripointe -Danypoint.password=Tslplabap@123 -Dtarget=TPH-MULE-DEV -Dtarget.type=server -Denv=Development -Dappname=cicd-test-app1'*/
  }
  else if(env.GIT_BRANCH == "QA")
  {
     def userAborted = false
    def jobName = currentBuild.fullDisplayName
    def mailToRecipients = 'rohit.singh@apisero.com'
   emailext body: '''
    Please go to console output of ${BUILD_URL}input to approve or Reject.<br>
 ''',    
    mimeType: 'text/html',
    subject: "[Jenkins] ${jobName} Build Approval Request",
    from: "rksinghkatras1234@gmail.com",
    to: "${mailToRecipients}",
    recipientProviders: [[$class: 'CulpritsRecipientProvider']]
 echo "Building1"
 try { 
    userInput = input submitter: 'vagrant', message: 'Do you approve?'
 } catch (org.jenkinsci.plugins.workflow.steps.FlowInterruptedException e) {
   cause = e.causes.get(0)
   echo "Aborted by " + cause.getUser().toString()
   userAborted = true
    echo "SYSTEM aborted, but looks like timeout period didn't complete. Aborting."
 }
    if (userAborted) {
  currentBuild.result = 'ABORTED'
 } else {
  echo "Building2"
 }
   echo 'Deploying mule project due to the latest code commit in QA branch…'
    echo 'Deploying to the QA environment….'
    /*bat 'mvn clean deploy -DmuleDeploy -DskipTests -Dmule.version=4.3.0 -Danypoint.username=rohit_tripointe -Danypoint.password=Tslplabap@123 -Dtarget=TPH-MULE-DEV -Dtarget.type=server -Denv=Development -Dappname=cicd-test-app1'*/
  }
   else if(env.GIT_BRANCH == "main")
  {
  	echo 'Deploying mule project due to the latest code commit in Prod branch…'
    echo 'Deploying to the Production environment….'
    /*bat 'mvn clean deploy -DmuleDeploy -DskipTests -Dmule.version=4.3.0 -Danypoint.username=rohit_tripointe -Danypoint.password=Tslplabap@123 -Dtarget=TPH-MULE-DEV -Dtarget.type=server -Denv=Development -Dappname=cicd-test-app1'*/
  }
  else
  {
   echo "Branch not expected."
    echo "New Change"
  }
}

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
             body: "Build Successful ${env.BUILD_URL}"
    }
}
}
