pipeline{
agent any
environment{
IMAGE_NAME='jenkins-web-app'
CONTAINER_NAME='jenkins-web-container'
HOST_PORT='8085'
}
stages{
stage('Checkout') {
steps {
git branch: 'main',url:'https://github.com/sunil18-droid/jenkins-advanced-task.git'
}
}
stage('Build'){
steps{
echo 'Building application....'
sh 'ls -l'
}
}
stage('Test') {
steps{
echo'Testing application files...'
sh 'test -f index.html'
sh 'test -f Dockerfile'
}
}
stage('Docker Build'){
steps {
sh 'docker build -t jenkins-web-app:${BUILD_NUMBER} .'
}
}
stage('Deploy') {
steps {
sh '''
docker rm -f jenkins-web-container || true
docker run -d  -p 8085:80 
--name jenkins-web-container
jenkins-web-app:${build_number}
'''
}
}
stage('verify') {
steps {
sh 'curl -f http://localhost:${8085}'
}
}
}
post {
success {
echo 'CI/CD Pipeline completed successfully!'
}
failure {
echo 'CI/CD Pipeline failed. Check the console output.'
}
}
}
