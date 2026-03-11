pipeline {
    agent any

    parameters {
        choice(name: 'Backend_Count', choices: ['1', '2'], description: 'Number of backend containers')
    }

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t backend-app backend'
            }
        }

        stage('Deploy Containers') {
            steps {
                sh '''
                docker rm -f backend1 backend2 || true

                if [ "$Backend_Count" = "1" ]; then
                    docker run -d --name backend1 backend-app
                else
                    docker run -d --name backend1 backend-app
                    docker run -d --name backend2 backend-app
                fi
                '''
            }
        }

    }
}
