pipeline {
environment {
imagename = "etzi71/jenkins"
registryCredential = '9008c74f-4647-40cd-b983-a85a9f0ffffa'
dockerImage = ''
}
agent any
stages {
stage('Cloning Git') {
steps {
git([url: 'https://github.com/etzi71/jenkins.git', branch: 'master', credentialsId: '9008c74f-4647-40cd-b983-a85a9f0ffffa'])
}
}
stage('Building image') {
steps{
script {
dockerImage = docker.build imagename
}
}
}
stage('Deploy Image') {
steps{
script {
docker.withRegistry( '', registryCredential ) {
dockerImage.push("$BUILD_NUMBER")
dockerImage.push('latest')
}
}
}
}
stage('Remove Unused docker image') {
steps{
sh "docker rmi $imagename:$BUILD_NUMBER"
sh "docker rmi $imagename:latest"
}
}
}
}
