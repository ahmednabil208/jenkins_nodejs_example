pipeline{
    agent any

    stages{
        stage('preperation'){
            steps{
                git 'https://github.com/ahmednabil208/jenkins_nodejs_example.git'
                }

            }

        stage('build'){
            steps{
                sh 'docker build -t ahmednabil20/nodejs_img:lts .'
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                     sh "docker login -u $USERNAME -p $PASSWORD"
                }
                sh 'docker push ahmednabil20/nodejs_img:lts'    
            }
        }
        stage('Start Container'){
            steps{
                sh 'docker stop nodejs_app || true'
                sh 'docker rm -f nodejs_app || true'
                sh 'docker run -d -p 3000:3000 --name nodejs_app  ahmednabil20/nodejs_img:lts'
            }
        }
    }
}

