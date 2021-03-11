pipeline {
    agent any
    triggers { pollSCM('* * * * *') }
    stages {
        // implicit checkout stage
        // stage('Checkout') {
        //     steps {
        //         git branch: 'main', url: 'https://github.com/tsuyo/jgsu-spring-petclinic.git'
        //     }
        // }

        stage('Build') {
            steps {
                sh './mvnw clean package'
                // sh 'true'
            }
        }
    }

    // post after stages, for entire pipeline, is also an implicit step albeit with explicit config here,
    // unlike implicit checkout stage
    post {
        always {
            junit '**/target/surefire-reports/TEST-*.xml'
            archiveArtifacts 'target/*.jar'
        }
        // changed {
        //     emailext subject: "Job \'${JOB_NAME}\' (build ${BUILD_NUMBER}) ${currentBuild.result}",
        //       body: "Please go to ${BUILD_URL} and verify the build",
        //       attachLog: true,
        //       compressLog: true,
        //       to: "test@jenkins",
        //       recipientProviders: [upstreamDevelopers(), requestor()]
        // }
    }
}
