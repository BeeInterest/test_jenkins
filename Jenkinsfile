pipeline {
    agent {
        docker {
            image 'python'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    
    environment {
        POSTGRES_DB = 'db'
        POSTGRES_USER = 'postgress'
        POSTGRES_PASSWORD = 'password'
        POSTGRES_HOST_AUTH_METHOD = 'trust'
    }

    stages {
        stage('app') {
            steps {
                script {
                    sh 'pip install psycopg2 mimesis faker'
                    sh 'python func_db.py'
                }
            }
            post {
                always {
                    archiveArtifacts 'result.txt'
                }
                success {
                    echo 'Build successful!'
                }
                failure {
                    echo 'Build failed!'
                }
            }
        }
    }
}
