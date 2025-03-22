pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the project using Jenkins-configured Maven...'
                git branch: 'main', url: 'https://github.com/saamy45/6.2C-JENKIN.git'
            }
        }

         stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Running code analysis with SonarQube...'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan with OWASP Dependency Check...'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying the application to staging"
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on staging"
            }
        }

        stage('Deploy to Production') {
            steps {
                 echo "Deploying application to production"
            }
        }
    }

    post {
        success {
            script {
                def powershellCommand = '''
                $SMTPServer = "smtp.gmail.com"
                $SMTPPort = 587
                $SMTPFrom = "sambhav4808.be23@chitkara.edu.in"
                $SMTPTo = "sambhavv23@gmail.com"
                $SMTPSubject = "Successfully Execution of Pipeline!"
                $SMTPBody = "Pipeline has been executed successfully"
                $SMTPUsername = "sambhav4808.be23@chitkara.edu.in"
                $SMTPPassword = "HITMAN454545/" 
                $SMTPEnableSSL = $true

                $SMTPClient = New-Object Net.Mail.SmtpClient($SMTPServer, $SMTPPort)
                $SMTPClient.EnableSsl = $SMTPEnableSSL
                $SMTPClient.Credentials = New-Object System.Net.NetworkCredential($SMTPUsername, $SMTPPassword)
                $SMTPClient.Send($SMTPFrom, $SMTPTo, $SMTPSubject, $SMTPBody)
                '''
                powershell(powershellCommand)
            }
            echo "SUCCESSFULL!"
        }

        failure {
            script {
                def powershellCommand = '''
    
                 $SMTPServer = "smtp.gmail.com"
                $SMTPPort = 587
                $SMTPFrom = "sambhav4808.be23@chitkara.edu.in"
                $SMTPTo = "sambhavv23@gmail.com"
                $SMTPSubject = "Unsuccessfully Execution of Pipeline!"
                $SMTPBody = "Pipeline does not execute successfully"
                $SMTPUsername = "sambhav4808.be23@chitkara.edu.in"
                $SMTPPassword = "HITMAN454545/" 
                $SMTPEnableSSL = $true

                $SMTPClient = New-Object Net.Mail.SmtpClient($SMTPServer, $SMTPPort)
                $SMTPClient.EnableSsl = $SMTPEnableSSL
                $SMTPClient.Credentials = New-Object System.Net.NetworkCredential($SMTPUsername, $SMTPPassword)
                $SMTPClient.Send($SMTPFrom, $SMTPTo, $SMTPSubject, $SMTPBody)
                '''
                powershell(powershellCommand)
            }
            echo "FAILED!"
        }
    }
}
