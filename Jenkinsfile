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

stage('Deploy OnPremise') {
steps {
mail bcc: '', body: 'Build Successful', cc: '', from: '', replyTo: '', subject: 'Build Successful', to: 'rohit.singh@apisero.com'
}
}
}
}