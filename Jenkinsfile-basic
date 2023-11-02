pipeline{
    agent any
    stages{
        stage ('Package and Test Code'){
            steps{
                sh '''
                  mvn test
                  mvn package
                '''
            }
        }
    }
}    
