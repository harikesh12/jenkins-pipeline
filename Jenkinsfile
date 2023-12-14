pipeline{
    agent any
    tools{
        maven 'maven'
    }
    environment{
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
    }

}