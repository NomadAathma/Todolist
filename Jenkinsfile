pipeline {
    agent any

    stages {
        stage('Clear Workdirectory and Remove Files') {
            steps {
                sh 'rm -rf Todolist'
            }
        } 
        stage('Git Clone And Change Directory') {
            steps {
                sh 'git clone -b master https://github.com/NomadAathma/Todolist.git'
                sh 'cd Todolist'
            }
        }
         stage('Build') {
            steps {
                sh'docker build -t todoapp .'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker run -d -p 8000:8000 todoapp'
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
