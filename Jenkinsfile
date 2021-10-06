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
// Advice: don't define M2_HOME in general. Maven will autodetect its root fine.
withEnv(["JAVA_HOME=${ tool 'jdk-1.8.0_64bits' }", "PATH+MAVEN=${tool 'maven-3.2.1'}/bin:${env.JAVA_HOME}/bin"]) {

    // Apache Maven related side notes:
    // --batch-mode : recommended in CI to inform maven to not run in interactive mode (less logs)
    // -V : strongly recommended in CI, will display the JDK and Maven versions in use.
    //      Very useful to be quickly sure the selected versions were the ones you think.
    // -U : force maven to update snapshots each time (default : once an hour, makes no sense in CI).
    // -Dsurefire.useFile=false : useful in CI. Displays test errors in the logs directly (instead of
    //                            having to crawl the workspace files to see the cause).
    sh "mvn --batch-mode -V -U -e clean deploy -Dsurefire.useFile=false"

}