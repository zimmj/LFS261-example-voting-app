pipeline {
agent{
docker{
image 'maven:3.6.1-jdk-8-slim'
args '-v $HOME/.m2:/root/.m2'
}
}
stages{
stage('build'){
steps{
echo 'building worker app'
dir('worker'){
sh 'mvn compile'
}
}
}
stage('test'){
steps{
echo 'running unit tests on worker app'
dir('worker'){
sh 'mvn clean test'
}
}
}
stage('package'){
steps{
echo 'packaging worker app into a jarfile'
dir('worker'){
sh 'mvn package -DskipTests'
archiveArtifacts artifacts: '**/target/*.jar',
fingerprint:  true
}
}
}
}
post{
always{
echo 'the job is complete'
}
}
}
