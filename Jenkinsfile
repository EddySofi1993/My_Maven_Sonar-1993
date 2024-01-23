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
                        sh "${tool("SonarQube")}/bin/sonar-scanner \
                        -Dsonar.projectKey=My_Maven_Sonar-1993 \
                        -Dsonar.sources=. \
                        -Dsonar.java.binaries=target \
                        -Dsonar.host.url=http://3.106.252.125:9000/ \
                        -Dsonar.login=sqp_1498ebc583643fde0981587afaba76744a731442"
                         }
                }
        }
        stage("Nexus Upload") {
            steps{
                sh 'mvn -s settings.xml clean deploy'
            }
        }
        stage('deployment'){
            agent any
            steps{
                sh 'ansible-playbook -i inventory.yml deployment_playbook.yml -e "build_number=${BUILD_NUMBER}"'
            }
        }

    }
}

    
