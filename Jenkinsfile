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
                echo 'deploying!'
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'MyAWS',
                    accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                    secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]){
                        sh(script: 'aws s3 cp /var/lib/jenkins/workspace/Jenkins_pipeline/index.html s3://s3-udemy-jenkins-demo1-yomata/')
                }
            }
        }
        
        stage('test') {
            steps {
                echo 'testing'
                script {
                    def url = 'https://s3-udemy-jenkins-demo1-yomata.s3.ap-northeast-1.amazonaws.com/index.html'
                    def response = sh(script: "curl -s -o /dev/null -w '%{http_code}' '$url'", returnStdout: true)

                    if (response == '200') {
                        echo 'Test OK'
                    } else {
                        echo response
                        error 'Test NG'
                    }
                }
            }
        }
    }
}
