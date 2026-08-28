pipeline { 
    agent { 
        node { 
            label 'AGENT-1' 
        } 
    } 

    environment { 
        COURSE = "jenkins" 
    } 
    options {
        timeout(time: 10, unit: 'SECONDS')

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
                script { 
                    sh """
                        echo "hello depolying"
                        echo $COURSE
                        env
                        sleep 10
                    """
                } 
            } 
        } 
    } 

    post { 
        always {  
            echo 'I will always say Hello again!' 
            cleanWs()  
        } 

        success { 
            echo 'Run if pipeline success' 
        } 

        failure { 
            echo 'Run if pipeline failure' 
        } 
        aborted {
            echo "pipeline is aborted"
        }
    } 
}
}