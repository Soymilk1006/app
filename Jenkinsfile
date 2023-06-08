@Library('jenkins-shared-library')
def gv


pipeline {
    agent any
     tools {
        maven 'Maven-java' 
    }
    
    parameters {
        choice(name: 'VERSION', choices: ['1.1.0','1.1.2'], description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description:'')
    }
    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        
        stage("test"){
              steps {
                  script {
                        echo "Testing the application..."
                        echo "Executing pipeline for branch"
                  }
              }
              }
              
        stage("build jar") {
            steps {
                script {
                    echo "building jar"
              
                }
            }
        }
              
        stage("build image") {
            when {
                expression {
                    BRANCH_NAME == 'master'
                    buildJar()
                }
            }
                
            steps {
                script {
                    echo "building image"
                    buildImage 'legendlight/docker_image:jar-1.0'
                    dockerLogin()
                    dockerPush 'legendlight/docker_image:jar-1.0'
                  
                }
            }
        }
        stage("deploy") {
            input {
                message "Start deploying .."
                ok "Done"
                parameters {
                    choice(name:'ENV', choices:['dev','staging','pro'],description: '')
                }
            }
            steps {
                script {
                    echo "deploying ${ENV}"
                    gv.deployApp()
                }
            }
        }
    }   
}
