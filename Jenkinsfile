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
        stage ('Build Docker Image'){
            steps{
                sh '''
                   docker build -t mos87/java-maven-app:${BUILD_ID} .
                '''
            }
        }
        stage('Docker Push'){
            steps {
                withCredentials(
                    [usernamePassword
                        (credentialsId: 'dockerhub', passwordVariable: 'password', usernameVariable: 'username')]) {
                        sh "docker login -u ${env.username} -p ${env.password}"
                        sh 'docker push mos87/java-maven-app:${BUILD_ID}'
                    }
                }
        }        
    }
}    
