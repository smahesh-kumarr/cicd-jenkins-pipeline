pipeline {
    agent {
        label 'Jenkins-Dev'
    }
    environment {
        NAME = "Mahesh"
    }
    tools {
        maven 'mymaven'
    }
    stages {
        stage('build') {
            steps {
                sh 'mvn clean package'
                echo "Hello, $NAME"
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('test') {
            parallel {
                stage('testA') {
                    steps {
                        echo "This is test A"
                    }
                }
                stage('testB') {
                    steps {
                        echo "This is test B"
                    }
                }
            }
        }
    }
}
