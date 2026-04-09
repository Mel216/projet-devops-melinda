pipeline {
    agent any
    
    parameters {
        string(name: 'build_version', defaultValue: 'V1.0', description: 'Build version for Docker image')
    }
    
    environment {
        DOCKER_IMAGE = "abdelbakibouzaienne/demo-java-app:${params.build_version}"
        SONAR_URL = "http://sonarqube:9000"
    }
    
    stages {
        stage('Checkout') {
            steps {
                // In a real scenario, this would be a git checkout
                // For local demo, we assume the code is already there or checked out by Jenkins
                checkout scm
            }
        }
        
        stage('Build and Test') {
            steps {
                sh 'cd demo-java-app && mvn clean package'
            }
        }
        
        stage('Static Code Analysis') {
            steps {
                // Requires 'sonarqube' credential (Secret Text) in Jenkins
                withCredentials([string(credentialsId: 'sonarqube', variable: 'SONAR_AUTH_TOKEN')]) {
                    sh 'cd demo-java-app && mvn sonar:sonar -Dsonar.login=$SONAR_AUTH_TOKEN -Dsonar.host.url=${SONAR_URL}'
                }
            }
        }
        
        stage('Build and Push Docker Image') {
            steps {
                script {
                    // Requires 'dockerhub' credential (Username/Password) in Jenkins
                    sh 'cd demo-java-app && docker build -t ${DOCKER_IMAGE} .'
                    docker.withRegistry('https://index.docker.io/v1/', "dockerhub") {
                        docker.image("${DOCKER_IMAGE}").push()
                    }
                }
            }
        }
        
        stage('Update Helm Deployment') {
            steps {
                // Update the tag in values.yaml and push back to Git
                // Requires 'github' credential (Secret Text / PAT) in Jenkins
                withCredentials([string(credentialsId: 'github', variable: 'GITHUB_TOKEN')]) {
                    sh """
                        git config user.email "devops@example.com"
                        git config user.name "Jenkins Pipeline"
                        sed -i "s/tag: .*/tag: \\"${params.build_version}\\"/" helm/app/values.yaml
                        git add helm/app/values.yaml
                        git commit -m "Update image tag to ${params.build_version}"
                        git push https://${GITHUB_TOKEN}@github.com/your-username/your-repo.git HEAD:main
                    """
                }
            }
        }
    }
    
    post {
        always {
            cleanWs()
        }
    }
}
