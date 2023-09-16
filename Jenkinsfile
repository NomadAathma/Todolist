pipeline {
    agent any
    stages{
        stage("Cleaning repo"){
            steps{
                echo "Cleaning repo"
                sh "rm -rf *"
            }
        }
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
                sh "cd Todolist/"
        dir(path: "Todolist/") {
            sh "docker build -t my-image -f Dockerfile ."
        }
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

