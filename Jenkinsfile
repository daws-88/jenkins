pipeline {
    agent  {
        node {
            label 'AGENT-1'
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