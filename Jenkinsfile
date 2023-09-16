pipeline {
    agent any
    stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                sh "git clone -b master https://github.com/NomadAathma/Todolist.git"
                sh "cp -r Todolist/mynotes/build/* /var/www/html/"
            }
        }
        stage("Build"){
            steps {
                echo "Building the image"
                sh "cd /home/ubuntu/Todolist"
                sh "docker build -t my-note-app ."
            }
        }
        stage("Deploy"){
            steps {
                echo "Deploying the container"
                sh "docker run -d -p 8000:8000 my-note-app"

            }
        }
    }
}

