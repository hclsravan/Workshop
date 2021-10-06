pipeline {
    agent any
    tools {
        maven "Maven3"
    }
    stages {
        stage('Build') {
            steps {

                script {
                    def os = System.properties['os.name'].toLowerCase()
                    echo "OS: ${os}"                
                    if (os.contains("linux")) {
                      sh "mvn clean install -DskipTests" 
                    } else {
                      bat "mvn clean install -DskipTests"
                    }
                }

            }
        }
    }
}