pipeline {
    agent any

    environment{
        SONAR_TOKEN = "sqa_15771b5e67dfbcf6d6cf73049e646e1c14f9c46"
    }
    stages {
        stage('Build') {
            steps {
                echo "Build the code using Maven.."
                echo 'Tool: Maven'
                echo "mvn clean package"
                echo 'Build completed...'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo "Run unit tests using maven..."
                echo 'mvn test'
                echo "Run integration tests using maven integration test..."
                echo 'Tool: Maven'
                //echo 'Testing completed'
            }
            post {
                success {
                    // Send success notification email with logs attached
                    emailext(
                        from: 'injectsql001@gmail.com',
                        to: 's222337266@deakin.edu.au',
                        subject: 'Pipeline Success: Test stage',
                        body: 'The test stage of the Pipeline ran successfully.',
                        attachLog: true
                    )
                }
                failure {
                    // Send failure notification email with logs attached
                    emailext(
                        from: 'injectsql001@gmail.com',
                        to: 's222337266@deakin.edu.au',
                        subject: 'Pipeline Failure: Test stage',
                        body: 'The test stage of the Pipeline failed.',
                        attachLog: true
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo "Perfoming code analyses using SonarQube.."
                echo 'Tool: SonarQube'
                // echo "mvn sonar:sonar -Dsonar.token=${SONAR_TOKEN}"            
            }
        }
        stage('Security Scan') {
            steps {
                echo "Perform security scan..."
                echo 'Tool: OWASP ZAP'
                // echo "zap-cli --quick-scan --spider --self-contained http://localhost:8080/myapp"
            }
            post {
                success {
                    // Send success notification email with logs attached
                    emailext(
                        to: 's222337266@deakin.edu.au',
                        subject: 'Pipeline Success: Security scan stage',
                        body: 'The security scan stage of the Pipeline ran successfully.',
                        attachLog: true
                    )
                }
                failure {
                    // Send failure notification email with logs attached
                    emailext(
                        from: 'injectsql001@gmail.com',
                        to: 's222337266@deakin.edu.au',
                        subject: 'Pipeline Failure: Security scan stage',
                        body: 'The security scan stage of the Pipeline failed.',
                        attachLog: true
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo "Deploy the application to staging server in AWS EC2..."
                echo 'Tool: Secure Shell (ssh)'
                // echo 'ssh user@staging-server "cd /path/to/app && ./deploy.sh"'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo "Run integration tests on staging environment with selenium.."
                echo "Tool: Selenium"
            }
        }
        stage('Deploy to Production') {
            steps {
                echo "Deploy the application to production server in AWS EC2 instance..."
                echo 'Tool: Secure Shell (ssh)'
                // echo 'ssh user@production-server "cd /path/to/app && ./deploy.sh"'
            }
        }
    }
}
