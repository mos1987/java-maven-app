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
                        (credentialsId: 'dockerhub', passwordVariable: 'dockerhubpassword', usernameVariable: 'dockerhubusername')]) {
                        sh "docker login -u ${env.dockerhubusername} -p ${env.dockerhubpassword'}"
                        sh "docker push mos87/java-maven-app:${BUILD_ID}"
                    }
                }
        }        
    }
}    
