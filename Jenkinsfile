pipeline {
    agent any;

    stages {
        stage("Code Clone") {
            steps {
                git branch: 'master', url: 'https://github.com/LondheShubham153/two-tier-flask-app.git'
            }
        }

        stage("Build") {
            steps {
                script {
                    sh "docker build -t two-tier-flask-app ."
                }
            }
        }

        stage("Test") {
            steps {
                echo "Developer / Tester will provide test scripts..."
            }
        }
        stage("Push to Docker hub") {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: "dockerHubCreds",
                    passwordVariable: "dockerHubPass",
                    usernameVariable: "dockerHubUser")]) {
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag two-tier-flask-app ${env.dockerHubUser}/two-tier-flask-app"
                sh "docker push ${env.dockerHubUser}/two-tier-flask-app:latest"
                }
            }
        }

        stage("Deploy") {
            steps {
                script {
                    sh "docker-compose up -d"
                }
            }
        }
    }
}
