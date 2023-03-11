pipeline{

    agent any

    stages{

        stage('sonar quality status'){

            agent{

                docker {
                    image 'maven'
                }
            }

            steps{
                script{
                        withSonarQubeEnv(credentialsId: 'sonar-token') {
                            sh 'mvn clean package sonar:sonar'
                        }
                }
            }
        }

        stage('Quality Gate Status'){

            steps{

                script{
                        waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                }
            }
        }

        // stage('docker build & docker push to Nexus repo'){

        //     steps{

        //         script{
                        
        //         }
        //     }
        // }
    }
}