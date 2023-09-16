pipeline {

    agent any

    environment {
        registry = "ankithm/todo"
        registryCredential = 'dockerhub'
    }

    stages{
         stage('Clear Workdirectory and Remove Files') {
            steps {
                sh 'rm -r *'
                // Remove files in /var/www/html (adjust this path as needed)
         
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

        stage('Build App Image') {
          steps {
            script {
              dockerImage = docker.build registry + ":V$BUILD_NUMBER"
            }
          }
        }

        stage('Upload Image'){
          steps{
            script {
              docker.withRegistry('', registryCredential) {
                dockerImage.push("V$BUILD_NUMBER")
                dockerImage.push('latest')
              }
            }
          }
        }

        stage('Remove Unused docker image') {
          steps{
            sh "docker rmi $registry:V$BUILD_NUMBER"
          }
        }

    }


}
