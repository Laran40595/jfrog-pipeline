pipeline {

    agent any

    stages {

        stage('Clone Repo') {
            steps {
                git branch: 'main',
                url: 'https://github.com/Laran40595/jfrog-pipeline.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Publish to JFrog') {
            steps {
                sh '''
                jfrog rt upload "target/*.war" my-repo/ --flat=false
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully 🎉'
        }

        failure {
            echo 'Pipeline failed ❌ Check logs'
        }

        always {
            cleanWs()
        }
    }
}
