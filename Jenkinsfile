pipeline {
  agent  none
   
  stages {
   stage('Unit test'){
   agent {
   label 'apache'
   }
   steps{
   sh 'ant -f test.xml -v'
   junit 'reports/result.xml'
}
}
   stage ( 'build') {
   agent {
   label 'apache'
    steps{
      sh 'ant -f build.xml -v'
}
}
stage ('deploy'){
Agent {
label 'apache'
}
steps{
sh" cp /root/.jenkins/workspace/Javapipeline/dist/rectangle_${env.BUILD_NUMBER}.jar  /var/www/html/rectangles/all"
}
}

stage ("Running on Linux"){
agent{
label 'Linux'
}
steps {
sh "wget http://ec2-54-84-88-150.compute-1.amazonaws.com/rectangles/all/rectangle_${env.BUILD_NUMBER}.jar"
sh "java -jar rectangle_${env.BUILD_NUMBER}.jar 5 4"
}
}
stage("Test on Debian") {
      agent {
        docker 'openjdk:8u121-jre'
      }
      steps {
        sh "wget http://ec2-54-84-88-150.compute-1.amazonaws.com/rectangles/all/rectangle.${env.BUILD_NUMBER}.jar"
        sh "java -jar rectangle_${env.BUILD_NUMBER}.jar 3 4"
post {
always {
archiveArtifacts artifacts: 'dist/*.jar', fingerprint: true
}
}
}


