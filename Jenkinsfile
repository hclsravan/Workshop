node{
    stage('Scm Checkout'){
    git branch: 'main', credentialsId: 'workshop', url: 'https://github.com/hclsravan/Workshop.git'
}
    stage('Mvn Package'){
    def M2_HOME = tool name: 'maven-3', type: 'maven'
    def mvnCMD = "${M2_HOME}"
    bat 'mvn clean package'
}
     stage('Build Docker'){
     sh 'docker build -t bojja/my-app:${BUILD_NUMBER} .'
}
    stage('Push Docker Image'){
        
    withCredentials([string(credentialsId: 'docker', variable: 'docker')]) {
     sh "docker login -u bojja --password-stdin ${docker}"
}
     sh 'docker push bojja/my-app:${BUILD_NUMBER}'
  

}




}
