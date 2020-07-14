node {
    def app
    stage('Create the repository') {
        sh "sudo rm -rf wordpress_docker && sudo git clone https://github.com/Ishiven/wordpress_docker && cd wordpress_docker"
        sh "aws ecr delete-repository --repository-name test1 --region eu-west-1 && aws ecr create-repository --region eu-west-1 --repository-name test1"
    }

    stage ('Login to the repo') {
        sh "aws ecr get-login-password --region eu-west-1 | sudo docker login --username AWS --password-stdin 814323053068.dkr.ecr.eu-west-1.amazonaws.com"
    }
    stage('Build image') {
        sh "sudo docker build --build-arg APP_NAME=testapp -t 814323053068.dkr.ecr.eu-west-1.amazonaws.com/test1:latest -f ./Dockerfile ."
    }
    stage('Push image') {
        docker.withRegistry('https://814323053068.dkr.ecr.eu-west-1.amazonaws.com', 'ecr:eu-west-1:test1') {
            sh "sudo docker push 814323053068.dkr.ecr.eu-west-1.amazonaws.com/test1:latest"
        }
    }
}
