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
    }
}