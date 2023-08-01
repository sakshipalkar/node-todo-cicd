pipeline{
     agent {label 'dev' }
     stages{
         stage('Code'){
             steps{
                 git url: 'https://github.com/sakshipalkar/node-todo-cicd.git', branch: 'master'
             }
         }
         stage('Build'){
             steps{
                 sh 'docker build . -t 7387598439/node-todo-app-cicd:latest'
             }
         }
         stage('login and image push'){
             steps{
                 withCredentials([usernamePassword(credentialsId:'dockerhub',passwordVariable:'dockpass',usernameVariable:'dokuser')]){
                     sh "docker login -u ${env.dokuser} -p ${env.dockpass}"
                     sh "docker push 7387598439/node-todo-app-cicd:latest"
                 }
             }
         }
         stage('deploy'){
             steps{
                 sh 'docker-compose down && docker-compose up -d'
             }
         }
     }
     
}
