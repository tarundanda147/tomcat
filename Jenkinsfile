pipeline {
    agent { label 'slave101' }

    stages {
        stage('checkout') {
            steps {
                sh 'rm -rf hello-world-war'
                sh 'git clone https://github.com/tarundanda147/hello-world-war/'
            }
        }
        
        stage('build') {
            steps {
                dir("hello-world-war") {
                    sh 'echo "inside build"'
                    sh "docker build -t tomcat-war:${BUILD_NUMBER} ."
                }
            }
        }
        
        stage('push') {
            steps {
                withCredentials([usernamePassword(credentialsId: '9edb749c-52c9-40d2-9266-024789f72979', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh "docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}"
                    sh "docker tag tomcat-war:${BUILD_NUMBER} tarundevops147/tomcat:${BUILD_NUMBER}"
                    sh "docker push tarundevops147/tomcat:${BUILD_NUMBER}"
                }
            }
        }
    }
}   
