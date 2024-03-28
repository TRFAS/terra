pipeline {
    agent any
 
    stages {
        stage('Cloning') {
            steps {
                echo 'Cloining the code from the github repository.'
                git 'https://github.com/Rohit2k00/Insurence-project.git'

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
                sh 'sudo docker build -t rohitwasnik1112/star-insurance .'
           }

       }
       
        
       stage('Pushing') {
           steps {
               echo 'pushing that image to the DockerHub'
               withCredentilas([usernamePassword(credentialsId: 'Docker-pass', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
                  sh 'sudo docker login -u ${env.USERNAME} -p ${env.PASSWORD}'
                  sh 'sudo docker push rohitwasnik1112/star-insurance'
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
