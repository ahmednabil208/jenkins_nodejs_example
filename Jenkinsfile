pipeline {
    agent any

    stages {
        stage('dockerhub login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh 'echo $PASSWORD | docker login -u $USERNAME --password-stdin'
                }
            }
        }

        stage('CI') {
            steps {
                // Build with full Docker Hub repo name
                sh 'docker build -t ahmednabil20/nodejs_img:lts .'
                sh 'docker push ahmednabil20/nodejs_img:lts'
            }
        }

        stage('CD') {
            steps {
                sh 'docker stop node_app || true'
                sh 'docker rm node_app || true'
                sh 'docker run -d --name node_app -p 3000:3000 ahmednabil208/nodejs_img:lts'
            }
        }
    }
}
