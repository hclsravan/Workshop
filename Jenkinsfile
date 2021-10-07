node{
    stage('Scm Checkout'){
    git branch: 'main', credentialsId: 'workshop', url: 'https://github.com/hclsravan/Workshop.git'
}
    stage('Mvn Package'){
    def M2_HOME = tool name: 'M2_HOME', type: 'maven'
    def mvnCMD = "${M2_HOME}"
    sh 'mvn clean package'
}
}