
pipeline {
agent any
stages {
stage('Build') {
steps {
// Get some code from a GitHub repository
git url: 'https://github.com/sabu13/flaskdemo.git'
// Run Maven on a Unix agent.
script{
if(isUnix()){
sh "pip install -r requirements.txt"
}
else{
bat "pip install -r requirements.txt"
}
}
}
}
stage('Integration Test') {
steps {
// Run Maven on a Unix agent.
    script{
        if(isUnix()){
        sh "pytest"
        }
    else{
            bat "pytest"
    }
    }
}
}
stage('Docker Build') {
            steps {
                script{
                if(isUnix()){
                sh "docker build -t  saniasabu/newflaskapp ."
                }
                else{
                 bat "docker build -t saniasabu/newflaskapp ."
                 }
                 }
            }
        }
stage('Docker Push') {
            steps {
               withCredentials([usernamePassword(credentialsId:'dockerhub',passwordVariable: 'dockerHubPassword',usernameVariable:'dockerHubUser')]){
                bat "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                bat "docker push saniasabu/newflaskapp:latest"
                }
            }
    }
}}