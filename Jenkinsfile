pipeline {

    agent any

    stages {

        stage('Clone Git Repository') {

            steps {

                git branch: 'main',
                    url: 'https://github.com/Laran40595/samplejavaapp.git'

            }

        }

        stage('Maven Package') {

            steps {

                sh '/usr/share/maven/bin/mvn clean package'

            }

        }

        stage('Publish to JFrog Artifactory') {

            steps {

                rtUpload(
                    serverId: 'my-artifactory',
                    spec: '''
                    {
                        "files": [
                            {
                                "pattern": "target/sampleapp.war",
                                "target": "generic-local/"
                            }
                        ]
                    }
                    '''
                )

            }

        }

    }

}
