pipeline {
    agent any

    stages {
        stage('Clear Workdirectory and Remove Files') {
            steps {
            sh 'git clone -b master https://github.com/NomadAathma/Todolist.git'
                sh 'cd Todolist'
            sh'docker build -t todoapp .'
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
