pipeline {

     agent any

    triggers {
        cron('H */8 * * *') //regular builds
        pollSCM('* * * * *') //polling for changes, here once a minute
    }

    stages {
        stage('Checkout') {
            steps { //Checking out the repo
               checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'git-swainsa1-code', url: 'https://github.com/swainsa1-code/sample-java']]])
            }
        }
        stage('Unit Tests') {
            steps {
                script {
                    try {
                        sh 'rm -rf complete/build/test-results/test'
                        sh 'cd complete && ./gradlew test --no-daemon' //run a gradle task
                    } finally {
                        junit 'complete/build/test-results/test/*.xml' //make the junit test results available in any case (success & failure)
                    }
                }
            }
        }
        
    }
       
    post {
        always { //Send an email to the person that broke the build
           echo 'Post buid Activity'
        }
   
    }
}
