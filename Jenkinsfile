pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello from github webhook trigger'
            }
        }
        
        stage('build') {
            steps {
                echo 'buildiing'
            }
        }
        
        stage('deploy') {
            steps {
                echo 'deploying'
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'MyAWS',
                    accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                    secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]){
                        sh(script: 'aws s3 cp /var/lib/jenkins/workspace/Jenkins_pipeline/index.html s3://s3-udemy-jenkins-demo1-yomata/')
                }
            }
        }
        
        stage('release') {
            steps {
                echo 'releaseing'
            }
        }
    }
}
