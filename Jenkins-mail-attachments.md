```Jenkinsfile
pipeline {
agent {label 'slave3'}
    stages {
        stage('environment details') {
            steps {
                echo bat(returnStdout: true, script: 'set')
            }
        }
        stage('test cases') {
            steps {
                echo bat(returnStdout: true, script: 'mvn test')
            }
        }
        stage('Sent an Email') {
            steps {
                emailext(to: 'krishna.raj@tisteps.co,vignesh.muthiyapillai@tisteps.co,noor.mohammed@tisteps.co', 
                        replyTo:'krishna.raj@tisteps.co,vignesh.muthiyapillai@tisteps.co,noor.mohammed@tisteps.co', 
                        subject: " Email Report from-'${env.JOB_NAME}'",
                        attachmentsPattern: 'target/surefire-reports/emailable-report.html');
            }
         }
    }
}


```
