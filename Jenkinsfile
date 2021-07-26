
pipeline {
agent any
stages {
stage('Build Application') {
    
steps {
     script {
                    if (env.BRANCH_NAME == 'main') {
                        echo 'I only execute on the master branch'
                    } else {
                        echo env
                    }
                }
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
