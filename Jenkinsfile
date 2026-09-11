pipeline {
    agent {
        node {
            label 'AGENT-1'
        }
    }
    environment {
        COURSE ="jenkins"
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
                      echo $COURSE
                      sleep 10
                      env 

                     echo "Hello ${params.PERSON}"
                     echo "Biography: ${params.BIOGRAPHY}"
                     echo "Toggle: ${params.DEPOLY}"
                     echo "Choice: ${params.CHOICE}"
                     echo "Password: ${params.PASSWORD}"
                       """
                }
            }
        }
        stage('Test') {
            steps {
                echo "Hello Test"
            }
        }
        stage('Depoly') {
            input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
            }
            // when {
            //     expression {
            //          "$params.DEPLOY == true"
            //                }
            //     }

            steps {
                echo "Hello Depolying"         
            }
        }
    }
    post {
        always { 
            echo 'I will always say Hello'
            cleanWs()
        }
        success {
            echo 'Run if pipeline success' 
        }
        failure {
            echo 'Run if pipeline failure' 
        }
        aborted {
            echo 'pipeline is aborted'
        }
    }
}