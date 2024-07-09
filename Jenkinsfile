pipeline {
    agent any
    stages{
        stage('Build Maven'){
            steps{
                git url:'https://github.com/QuinlanVic/cicdakshat/', branch: "master"
               sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t quinlan89/endtoendproject25may:v1 .'
                }
            }
        }
        stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push quinlan89/endtoendproject25may:v1'
                }
            }
        } 
        stage('Deploy') {
            steps {
               script {
                    sh "docker run -dt -p 8989:80 --name finalcontainer89 quinlan89/endtoendproject25may:v1"
                }
            }
        }
    }
}
