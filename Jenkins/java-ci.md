```groovy 
pipeline {
    agent any

    environment {
        VERSION = "1.0.${BUILD_NUMBER}"
        DOCKER_IMAGE = "your-jfrog-repo/your-app:${VERSION}"
        MAVEN_OPTS = "-Dmaven.test.failure.ignore=false"
    }

    tools {
        maven 'MAVEN_3'
        jdk 'JDK_11'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Checkstyle') {
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
            post {
                always {
                    recordIssues tools: [checkStyle(pattern: '**/target/checkstyle-result.xml')]
                }
            }
        }

        stage('OWASP Dependency Check') {
            steps {
                sh 'mvn org.owasp:dependency-check-maven:check'
            }
            post {
                always {
                    publishHTML([
                        allowMissing: false,
                        alwaysLinkToLastBuild: true,
                        keepAll: true,
                        reportDir: 'target/dependency-check-report',
                        reportFiles: 'dependency-check-report.html',
                        reportName: 'OWASP Dependency Check'
                    ])
                }
            }
        }

        stage('SonarQube Scan') {
            environment {
                SONARQUBE_SCANNER_PARAMS = '-Dsonar.projectKey=your-app -Dsonar.projectVersion=${VERSION}'
            }
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Run JUnit Tests') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Build & Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'JFROG_CREDENTIALS', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh '''
                        echo "$PASSWORD" | docker login your-jfrog-url -u "$USERNAME" --password-stdin
                        docker build -t ${DOCKER_IMAGE} .
                        docker push ${DOCKER_IMAGE}
                    '''
                }
            }
        }

        stage('Update Helm Chart Version (External Repo)') {
            agent {
                docker {
                    image 'alpine/git'
                    args '-v $HOME/.ssh:/root/.ssh'
                }
            }
            environment {
                REPO_URL = 'git@github.com:your-org/helm-charts.git'
                CHART_PATH = 'helm/your-app'
            }
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: 'GIT_SSH_KEY', keyFileVariable: 'SSH_KEY')]) {
                    sh '''
                        mkdir -p ~/.ssh
                        cp ${SSH_KEY} ~/.ssh/id_rsa
                        chmod 600 ~/.ssh/id_rsa
                        ssh-keyscan github.com >> ~/.ssh/known_hosts

                        git clone ${REPO_URL}
                        cd helm-charts/${CHART_PATH}
                        sed -i "s/^version:.*/version: ${VERSION}/" Chart.yaml
                        sed -i "s/^appVersion:.*/appVersion: \\"${VERSION}\\"/" Chart.yaml
                        git config user.email "ci@yourdomain.com"
                        git config user.name "Jenkins CI"
                        git add Chart.yaml
                        git commit -m "CI: Bump Helm chart version to ${VERSION}" || echo "No changes"
                        git push origin main
                    '''
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully"
        }

        failure {
            mail to: 'dev-team@yourcompany.com',
                 subject: "❌ Jenkins Build Failed - ${JOB_NAME} #${BUILD_NUMBER}",
                 body: """
Build Failed: ${JOB_NAME} #${BUILD_NUMBER}
URL: ${BUILD_URL}

Please check the Jenkins logs for more details.
"""
        }
    }
}
```
