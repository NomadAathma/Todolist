pipeline {
    agent any

    stages {
        stage('Clear Workdirectory and Remove Files') {
            steps {
                sh 'rm -r *'
                // Remove files in /var/www/html (adjust this path as needed)
                sh 'rm -rf /var/www/html/*'
            }
        }

        stage('Clone Repository and Change Directory') {
            steps {
                // Clone the GitHub repository
                sh 'git clone -b master  https://github.com/NomadAathma/Todolist.git '

                // Change directory to Todolist
               sh 'cd Todolist'
            }
        }

        stage('Copy Files to /var/www/html') {
            steps {
                // Copy files from Todolist/mynotes/build to /var/www/html
                sh 'cp -r Todolist/mynotes/build/* /var/www/html/'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build a Docker image with the tag 'todo'
                sh 'docker build -t todo .'
            }
        }

        stage('Run Docker Container') {
            steps {
                // Run a Docker container with the name 'todo' and publish port 8000
                sh 'docker run -d -p 8000:8000 --name todo todo'
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
