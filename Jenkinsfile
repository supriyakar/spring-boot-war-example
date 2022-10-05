pipeline {
    agent any
     tools {
        maven 'Maven' 
        }
    stages {
        stage("Test"){
            steps{
                // mvn test
                sh "mvn test"
                // slackSend channel: 'youtubejenkins', message: 'Job Started'
                
            }
            
        }
        stage("Build"){
            steps{
                sh "mvn package"
                
            }
            post{
                success{
                    archiveArtifacts artifacts: '**/*.war'
                }
                
            }
            
        }
        
        stage("Deploy on Prod"){
             input {
                message "Should we continue?"
                ok "Yes we Should"
            }
            
            steps{
                // deploy on container -> plugin
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://3.82.117.231:8080')], contextPath: app, war: '**/*.war'
                //deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://172.17.0.2:8080')], contextPath: null, war: '**/*.war'
                
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
            
        }
        failure{
            echo "========pipeline execution failed========"
             
        }
    }
}
