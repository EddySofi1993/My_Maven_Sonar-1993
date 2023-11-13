pipeline{
    agent any
    tools {
        maven 'My_Maven'
    }
    stages{
        stage('git checkout'){
            steps{
            checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/EddySofi1993/My_Maven_Sonar-1993.git']])
        }
    }
        stage("Build") {
            steps{
                sh 'mvn clean install'
            }
        }
         stage("SonarQube"){
            steps{
                    withSonarQubeEnv("SonarQube") {
                        sh "${tool("SonarScanner")}/bin/sonar-scanner \
                        -Dsonar.projectKey=My_Maven_Sonar-1993 \
                        -Dsonar.sources=. \
                        -Dsonar.java.binaries=target \
                        -Dsonar.host.url=http://52.62.2.97:9000/ \
                        -Dsonar.login=sqp_95794de8397f53e130cef5944bcbd96fb36ace72"
                         }
                }
        }
    }
    
}
       
