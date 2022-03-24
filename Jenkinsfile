pipeline {
    agent any

    parameters {
        choice(name: 'BuildTool', choices: ['Maven', 'Gradle'], description: '')
    }

    stages {
        stage('Build') {
            steps {
                script {
                    git 'https://github.com/AlexBezsh/builders.git'
                    if (params.BuildTool == 'Maven') {
                        bat 'mvn clean package'
                    } else {
                        bat 'gradle clean build -Penv=RELEASE'
                    }
                }
            }
        }

        stage('Deploy to QA') {
            steps {
                script {
                    deploy adapters: [tomcat9(credentialsId: 'tomcat-id', path: '', url: 'http://localhost:8181')], contextPath: '/hello', onFailure: false, war: 'web/**/*.war'
                }
            }
        }

        stage('Deployment Check') {
            steps {
                bat 'curl -f http://localhost:8181/hello'
            }
        }

        stage('Cloud Deployment') {
            steps {
                script {
                    deploy adapters: [tomcat9(credentialsId: 'remote-tomcat', path: '', url: 'http://ec2-3-126-50-83.eu-central-1.compute.amazonaws.com')], contextPath: '/hello', onFailure: false, war: 'web/**/*.war'
                }
            }
        }
    }
}