pipeline {
agent any
environment {
IMAGE_NAME='jenkins-web-app'
CONTAINER_NAME='jenkins-web-container'
HOST_PORT = '8085'
}
stages{
stage('Checkout') {
steps {
echo 'Checking out source code...'
git branch: 'main',
url:'http://github.com/sunil18-droid/jenkins-advanced-task.git'
}
}
stage('Build'){
steps {
echo 'Checking project files...'
sh 'ls -l'
}
}
stage('Test'){
steps {
echo 'Testing required files...'
sh 'test -f index.html'
sh 'test -f Dockerfile'
echo 'File tests passed!'
}
}
stage('Docker Build'){
steps {
echo 'Building Docker image...'
sh 'docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} .'
}
}
stage('Deploy'){
steps {
echo 'Deploying applications...'
sh 'docker rm -f ${CONTAINER_NAME}  || true'
sh 'docker run -d -p ${HOST_PORT}:80 --name ${CONTAINER_NAME} ${IMAGE_NAME}:${BUILD_NUMBER}'
}
}
stage('verify'){
steps{
echo'Verifying deployment...'
sh 'sleep 3'
sh 'curl -f http://localhost:${HOST_PORT}'
sh 'docker ps'
echo 'Application deployed successfully!'
}
}
}
post {
success {
echo 'CI/CD Pipeline completed successfully!'
}
failure {
echo 'CI/CD Pipeline failed. Check the  console output.'
}
always{
echo 'Pipeline execution completed.'
}
}
}
