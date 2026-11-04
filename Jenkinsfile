
pipeline {
    agent any

    environment {
        COURSE = "jenkins"
    }

    options {
        timeout(time: 10, unit: 'MINUTES')
        disableConcurrentBuilds()
    }

    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
        booleanParam(name: 'DEPOLY', defaultValue: true, description: 'Toggle this value')
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }

    stages {
        stage('Build') {
            steps {
                script {
                    sh """
                        echo "Hello Test"
                        echo \$COURSE
                        sleep 10
                        env
                        echo "Hello ${params.PERSON}"
                        echo "Biography: ${params.BIOGRAPHY}"
                        echo "Toggle: ${params.DEPOLY}"
                        echo "Choice: ${params.CHOICE}"
                    """
                }
            }
        }

        stage('Test') {
            steps {
                echo "Hello Test"
            }
        }

        stage('Deploy') {
            when {
                expression {
                    params.DEPOLY == true
                }
            }
            input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
            }
            steps {
                echo "Hello Deploying"
            }
        }
    stage('exit') {
        steps {
            script {
                sh """
                    echo "Hello Test"
                    
                """
              }
            }
        }
    }

    post {
        always {
            echo 'I will always say Hello'
            cleanWs()
        }

        success {
            echo 'Pipeline executed successfully'

            withCredentials([
                string(credentialsId: 'slack-auth', variable: 'SLACK_WEBHOOK')
            ]) {
                sh '''
                    curl -sS -X POST \
                    -H 'Content-type: application/json' \
                    --data '{"text":"SUCCESS: Jenkins pipeline executed successfully!"}' \
                    "$SLACK_WEBHOOK"
                '''
            }
        }

        failure {
            echo 'Pipeline failed'

            withCredentials([
                string(credentialsId: 'slack-auth', variable: 'SLACK_WEBHOOK')
            ]) {
                sh '''
                    curl -sS -X POST \
                    -H 'Content-type: application/json' \
                    --data '{"text":"FAILURE: Jenkins pipeline failed!"}' \
                    "$SLACK_WEBHOOK"
                '''
            }
        }

        aborted {
            echo 'Pipeline is aborted'
        }
    }
}
