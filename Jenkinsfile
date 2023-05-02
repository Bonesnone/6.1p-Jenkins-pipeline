pipeline {
    agent any
    environment {
        AGENT_NAME='Jye'
        PROJECT_NAME='6.2c-Jenkins-pipeline'
        LINUX_DIRECTORY_PATH='/usr/lib/jenkins/'
        WINDOWS_DIRECTORY_PATH='C:\Users\Jenkins\AppData\Local\Jenkins'
        TESTING_ENVIRONMENT='C:\Users\Jenkins\AppData\Local\Jenkins'
        PRODUCTION_ENVIRONMENT='Dockerhub'
        SNYK_NAME='Snyk-test-6.2c'
        SNYK_TOKEN='15a91d71-3e72-4997-ae13-f0705c310275'
    }
    stages {
        stage('1: Build') {
            steps {
                echo 'Fetch the source code from the directory path specified by the environment variable'
                echo 'Compile the code and generate any necessary artifacts'
            }
        }
        stage('2: Unit and Integration Tests') {
            steps {
                echo 'Unit tests'
                echo 'Integration tests'
            }
            post {
                success {
                    echo 'success!'
                    mail to: "s222134604@gmail.com"
                    subject: "Build status successful!"
                    body: "Congratulations, build ${BUILD_NUMBER} has passed testing inspection."
                }
            }
        }
        stage('3: Code Analysis') {
            steps {
                echo 'Ensure static code analysis meets industry standards'
            }
        }
        stage('4: Security Scan') {
            steps {
                echo 'Inspect code for security flaws, according to Synk database'
                snykSecurity (
                    snkyInstallation: "<%{SNYK_NAME}>",
                    snykTokenID: '<%{SNYK_TOKEN}>',
                    projectName: '%{PROJECT_NAME}',
                    failOnError
                )
            }
            post {
                success {
                    echo 'success!'
                    mail to: "s222134604@gmail.com"
                    subject: "Build status successful!"
                    body: "Congratulations, build ${BUILD_NUMBER} has passed security requirements."
                }
            }
        }
        stage('5: Deploy to staging server') {
            steps {
                echo "waiting for approval of ${AGENT_NAME}.."
                sleep 3
                echo 'Testing environment:'
                echo "${TESTING_ENVIRONMENT}"
                echo 'uploading to dockerhub'
            }
        }
        stage('6. Staging integration tests') {
            steps {
                echo "Reapplying checks with security measures."
                snykSecurity (
                    snkyInstallation: "<%{SNYK_NAME}>",
                    snykTokenID: '<%{SNYK_TOKEN}>',
                    projectName: '%{PROJECT_NAME}',
                    failOnError
                )
            }
        }
        stage('7. Deploy to production') {
            steps {
                echo 'Production environment:'
                echo "${PRODUCTION_ENVIRONMENT}"
                echo 'Finished!'
            }
        }
    }
}
