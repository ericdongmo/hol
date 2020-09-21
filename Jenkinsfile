pipeline {
    agent any
    tools {
        maven 'M2_HOME'
    }

    stages {
               
         stage('build') {
            steps {
                echo 'Hello build'
                sh 'mvn clean'
                sh 'mvn install'
                sh 'mvn package'
            }
        }
         stage('deploy') {
            steps {
                sh 'mvn test'
            }
        }
         stage('buld and publish image') {
        steps {
            script {
                checkout scm
                docker.withRegistry('', 'DockerID') {
                def customImage = docker.build("ericdongmo/hol-pipeline:${env.BUILD_ID}")
                customImage.push()    
            }
        }
                
        }
}
   }
}
