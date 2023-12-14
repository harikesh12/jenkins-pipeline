pipeline{
    agent any
    tools{
        maven 'maven'
    }
    environment{
        scanner_home =  tool 'sonar-scanner'
        maven_home = tool 'maven'
    }
    stages{
        stage('git checkout'){
            steps{
                 git 'https://github.com/harikesh12/hello-world.git'
            }
        }
        stage('Maven Junit test'){
            steps{
                 sh "${maven_home}/bin/mvn clean test"
            }
        }
        stage('Maven Build'){
            steps{
                 sh "${maven_home}/bin/mvn clean package"
            }
        }
        stage('SonarQube-QualityCheck'){
            steps{
                 withSonarQubeEnv('sonar-server') {
                   sh ''' ${scanner_home}/bin/sonar-scanner -Dsonar.projectName=cicd-axa \
                       -Dsonar.projectKey=cicd-axa -D sonar.java.binaries=**/target/classes ''' 
    // some blocksonar.projectKey
             }
            }
        }
        stage('print'){
            steps{
                   sh '''echo ${scanner_home} '''
    // some blocksonar.projectKey
            }
        }
    }

}
