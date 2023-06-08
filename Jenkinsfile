library identifier:'jenkins-shared-library@main', retriever:modernSCM(
    [$class:'GitSCMSource',
     remote:'https://github.com/Soymilk1006/jenkins-shared-library.git',
     credentialsId:'Github'
    ]                                                                                                                                                                                                               
)

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
                        echo "again"
                        
                      
                  }
              }
              }
              
        stage("build jar") {
            steps {
                script {
                    echo "building jar"
                      buildJar()
              
                }
            }
        }
              
        stage("build image") {
            when {
                expression {
                    BRANCH_NAME == 'master'
                  
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
            steps {
                script {
                    echo "deploying..."
                    gv.deployApp()
                }
            }
        }
    }   
}
