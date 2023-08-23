pipeline{
    agent any
    stages{
        stage("sonar quality check"){
            // agent {
            //     docker {
            //         image 'openjdk:11'
            //     }
            // }
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-token') {
                             sh 'chmod +x gradlew'
                             sh './gradlew sonarqube'
                    }

                    timeout(time:1, unit: 'HOURS') {
                        def checkStatus = waitForQualityGate()
                        if (checkStatus.status != 'OK') {
                            error "Pipeline aborted due to quality gate failure: ${checkStatus.status}"                        
                        }
                    }
                }
            }

            

        }
    }

}