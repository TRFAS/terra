pipeline {
    agent any
 
    stages {
        stage('Cloning') {
            steps {
                echo 'Cloining the code from the github repository.'
                git 'https://github.com/TRFAS/terra.git'

            }
        }
        
        
        stage('Building') {
            steps {
                echo 'Building the given code by using maven'
                sh 'mvn install'
            }
            
        }
        
        
       stage('Image Creating') {
           steps {
                echo 'creating an image using docker'
                sh 'sudo docker build -t dineshreddyramala/insure_project.'
           }

       }
       
        
       stage('Pushing') {
           steps {
               echo 'pushing that image to the DockerHub'
               withCredentials([usernamePassword(credentialsId: '4fc5f42e-7635-48f7-a096-07b75b5f4324', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
               sh 'docker login -u {USERNAME} -p {PASSWORD}'
               sh 'docker push dineshreddyramala/insure_project'
                      }
              
                 }
               }
        
        stage('Deploying') {
            steps {
                echo 'Deploying that application to the production server'
                sh 'sudo ansible-playbook /home/ubuntu/Insurence-project/playbook.yaml'
              }
        }
    }
}
