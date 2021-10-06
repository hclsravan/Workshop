node{
    stage('Scm Checkout'){
    git credentialsId: 'git', url: 'https://github.com/hclsravan/Workshop'
}
    stage('Mvn Package'){
    def M2_HOME = tool name: 'Maven', type: 'maven'
def mvnCMD = "${M2_HOME}"
    sh "${mvnCMD} clean package"
}
     stage('Build Docker'){
     sh 'docker build -t kishanpeddaboina/my-app:${BUILD_NUMBER} .'
}
    stage('Push Docker Image'){
        
    withCredentials([string(credentialsId: 'docker', variable: 'docker')]) {
     sh "docker login -u kishanpeddaboina --password-stdin ${docker}"
}
     sh 'docker push kishanpeddaboina/my-app:${BUILD_NUMBER}'
  

}




}
node{
    stage("test"){
        sh "ipconfig"
    }
}