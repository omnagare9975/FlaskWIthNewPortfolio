pipeline{
    agent any
    stages{
        stage("CheckOut"){
            steps{
                git "https://github.com/omnagare9975/FlaskWIthNewPortfolio.git", branch: "main"
            }
        }
        stage("Building"){
            steps{
                sh "docker build -t pythonapp ."
            }
        }
        stage("Deploy"){
            steps{
                sh "docker run -d -p 3000:3000 pythonapp"
            }
        }
        stage("Push On DockerHub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker tag pythonapp:latest ${env.dockerHubUser}/pythonapp:latest"
                sh "docker push ${env.dockerHubUser}/pythonapp:latest"
                echo 'image push ho gaya'
            }
        }
    }
}