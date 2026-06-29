pipeline {
    agent any
    
    environment{
       SCANNER_HOME= tool 'sonar-scanner'
         }
    stages {
        stage('Checkout') {
            steps {
                git branch:'master', url:'https://github.com/Chakrinitesh/node-js--sonar.git'
            }
        }
         stage('Dependencies') {
            steps {
                nodejs('Nodejs') {
                  sh "npm install"
              } 
           }
        }
         stage('Test') {
            steps {
                nodejs('Nodejs') {
                    sh "npm run test"
               } 
            }
        }
         stage('SonarQube Analysis') {
            steps {
               withSonarQubeEnv ('sonarqube'){
                   sh '''    $SCANNER_HOME/bin/sonar-scanner \
                            -Dsonar.projectName=node-js--sonar \
                            -Dsonar.projectKey=node-js--sonar \
                            -Dsonar.sources=.\
                            -Dsonar.tests=.\
                            -Dsonar.test.inclusions=**/*.test.js\
                            -Dsonar.javascript.lcov.reportPaths=coverage/lcov.info  
                '''
               } 
            }
        }
    }
}
