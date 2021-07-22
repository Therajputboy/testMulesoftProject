pipeline {
agent any
stages {
stage('Build Application') {
steps {
bat 'mvn clean install'
}
}

stage('Deploy OnPremise') {
steps {
echo 'Deploying mule project due to the latest code commit…'
echo 'Deploying to the configured environment….'
bat 'mvn clean deploy -DmuleDeploy -DskipTests -Dmule.version=4.3.0 -Danypoint.username=rohit_tripointe -Danypoint.password=Tslplabap@123 -Dtarget=TPH-MULE-DEV -Dtarget.type=server -Denv=Development -Dappname=cicd-test-app1 '
}
}
 post {
        always {
            script {
                BUILD_USER = getBuildUser()
            }
						emailext attachLog: true, 
			            mimeType: 'text/html',
						body:							"""<p>EXECUTED: Job <b>\'${env.JOB_NAME}:${env.BUILD_NUMBER})\'</b></p><p>View console output at "<a href="${env.BUILD_URL}"> 							${env.JOB_NAME}:${env.BUILD_NUMBER}</a>"</p> 	<p><i>(Build log is attached.)</i></p>""", 
						compressLog: true,
						recipientProviders: [[$class: 'DevelopersRecipientProvider'], 
						[$class: 'RequesterRecipientProvider']],
						replyTo: 'do-not-reply@company.com', 
						subject: "Status: ${currentBuild.result?:'SUCCESS'} - Job \'${env.JOB_NAME}:${env.BUILD_NUMBER}\'", 
							to: 'rohit.singh@apisero.com'
			}
	   }

}
}
