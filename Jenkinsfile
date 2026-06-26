pipeline {

    agent any

    stages {

        stage('clone git repo') {

            steps {

                git branch: 'feature-dotun-pipeline', url: 'https://github.com/bloomytech/samplejavaapp.git'

            }

        }

        stage('maven package'){

            steps{

                sh '/usr/share/maven/bin/mvn package'

            }

        }

       
        stage('publish to jfrog') {

            steps {

                rtUpload (

                    serverId: 'jfrog-dev',

                    spec: '''{

                        "files": [{

                        "pattern": "target/sampleapp.war",

                        "target": "generic-local/"

                        }]

                    }'''

                )

            }

        }

    }

}

