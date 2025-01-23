pipeline{
    agent{
        label 'DevServer'
    }
    stages{
        stage('build'){
            steps{
                sh 'mvn clean package'
            }

            post {
                success {
                    archiveArtificates artifacts: '**/target/*.war'
                }
            }
        }
        
    }
}