pipeline{
    agent any

    stages{
        stage('build'){
            steps{
                sh 'docker build -t ahmednabil20/nodejs_img:lts .'
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                     sh "echo $PASSWORD | docker login -u $USERNAME --password-stdin"
                }
                echo "$PASSWORD" | docker login -u "$USERNAME" --password-stdin    
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

