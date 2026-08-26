pipeline {
    agent {
    docker {
        label 'AGENT-'
    }
}
        stages {
            stage('build') {
                steps {
                    echo "Hello building"
                }
            }
             stage('test') {
                steps {
                    echo "Hello testing"
                }
            }
            
            stage('depoly') {
                steps {
                    echo "Hello deploying"
                }
            }
        }
}