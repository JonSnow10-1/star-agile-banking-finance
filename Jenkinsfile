pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M2_HOME"
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/JonSnow10-1/star-agile-banking-finance.git'

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"

            }        
        }
       stage('Generate Test Reports') {
           steps {
               publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/var/lib/jenkins/workspace/BankingProject/target/surefire-reports', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
                    }
            }
       stage('Create Docker Image') {
           steps {
               sh 'docker build -t ganesh36/banking-project-demo:1.0 .'
                    }
                }
       stage('Docker-Login') {
           steps {
               withCredentials([usernamePassword(credentialsId: 'Docker-login', passwordVariable: 'dockerpassword', usernameVariable: 'dockerlogin')]) { 
               sh 'docker login -u ${dockerlogin} -p ${dockerpassword}'
                                   }
                        }
                }
       
}
}
