pipeline{

    agent any

    stages{

        stage('Continous Download'){
            
            steps{
                git branch: 'main', url: 'https://github.com/clemenrance/Momo-cash.git'
            }
        }
        stage('Unit testing'){

            steps{
                sh 'mvn test'
            }
        }
        stage('Integration test'){

            steps{
                sh 'mvn verify -DskipUnitTests'
            }
        }
        stage('Maven Build'){

            steps{
                sh 'mvn clean install'
            }
        }
        stage('Static Code analysis'){

            steps{

                script{
                    withSonarQubeEnv(credentialsId: 'sonarqube-token'){
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }
        stage('Quality Gate Analysis'){

            steps{

                script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonarqube-token'
                }
            }
        }
        stage('Nexus Artificat Upload'){

            steps{

                script{
                 nexusArtifactUploader artifacts: [[artifactId: 'springboot', classifier: '', file: 'target/Uber.jar', type: 'jar']], credentialsId: 'nexus-auth', groupId: 'com.example', nexusUrl: '54.210.111.106:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'momo-cash-repo', version: '1.0.0'   
                }
            }
        }
    }
}