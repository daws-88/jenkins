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
        timeout(time: 10, unit: 'MINUTES')
        disableConcurrentBuilds()
     }
      parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
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
                script { 
                    sh """
                        echo "hello depolying"
                        echo $COURSE
                        env
                        sleep 10
                        echo "Hello ${params.PERSON}"
                        echo "Biography: ${params.BIOGRAPHY}"
                        echo "Toggle: ${params.TOGGLE}"
                        echo "Choice: ${params.CHOICE}"
                        echo "hello webhools"
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
