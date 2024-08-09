pipeline {
    agent any

    tools {
        maven "maven3"
        jdk "jdk17"
    }

    environment{

        SCANNER_HOME = tool "sonar-scanner"
    }

    stages {
        stage('Git checkout') {
            steps {
                git branch: 'main', credentialsId: 'git-cred', url: 'https://github.com/amitsahu0/Shopping-Cart.git'
            }
        }

        stage('Compile') {
            steps {
                sh "mvn compile"
            }
        }

        stage('Owasp DC') {
            steps {
                dependencyCheck additionalArguments: '--scan ./', odcInstallation: 'DC'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }

        stage('Sonarqube Scanner') {
            steps {
                withSonarQubeEnv('sonar') {
                   sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Shopping-Cart \
                   -Dsonar.java.binaries=target/classes \
                   -Dsonar.projectKey=Shopping-Cart '''
                }
            }
        }

        stage('Build Application and Push Artifact') {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'jdk17', maven: 'maven3', mavenSettingsConfig: 'maven-settings-default', traceability: true) {
                    sh "mvn deploy --DskipTests=true"
                }
            }
        }

        // stage('Hello') {
        //     steps {
        //         echo 'Hello World'
        //     }
        // }

        // stage('Hello') {
        //     steps {
        //         echo 'Hello World'
        //     }
        // }

        // stage('Hello') {
        //     steps {
        //         echo 'Hello World'
        //     }
        // }

        // stage('Hello') {
        //     steps {
        //         echo 'Hello World'
        //     }
        // }

        // stage('Hello') {
        //     steps {
        //         echo 'Hello World'
        //     }
        // }

        // stage('Hello') {
        //     steps {
        //         echo 'Hello World'
        //     }
        // }
    }
}
