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
        stage('SonarQube-Scanner'){
            steps{
                 withSonarQubeEnv('sonar-server') {
                //    sh ''' ${scanner_home}/bin/sonar-scanner -Dsonar.projectName=cicd-axa \
                //        -Dsonar.projectKey=cicd-axa -D sonar.java.binaries=**/target/classes ''' 
                // for this we have to define above properties in /var/lib/jenkins/tools/hudson.plugins.sonar.SonarRunnerInstallation/sonar-scanner/conf
                sh ''' ${scanner_home}/bin/sonar-scanner '''
 
             }
            }
        }
        // Webhook does not support loop back address i.e. jenkins and sonarqube should not be on same machine
        // Below step will only allow if quality gate condition is passed.
        stage('Quality-Gate '){
            steps{
                script{
                 waitForQualityGate abortPipeline: true, credentialsId: 'sonarqube'
                }
            }
        }
    }

}
