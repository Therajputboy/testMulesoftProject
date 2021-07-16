pipeline {
agent any
stages {
stage('Build Application') {
steps {
bat 'mvn clean install'
}
}

stage('Deploy CloudHub') {
steps {
echo 'Deploying mule project due to the latest code commit…'
echo 'Deploying to the configured environment….'
bat 'mvn clean deploy -DmuleDeploy -DskipTests -Dmule.version=4.3.0 -Danypoint.username=rksinghjuly -Danypoint.password=Tslplabap@123 -Denv=Sandbox -Dappname=cicd-test-app1 -Dbusiness=apisero -DvCore=Micro -Dworkers=1'
}
}
}
}