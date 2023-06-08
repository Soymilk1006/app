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
        stage("build jar") {
            steps {
                script {
                    echo "building jar"
                    gv.buildJar()
                }
            }
        }
        stage("build image") {
            steps {
                script {
                    echo "building image"
                    gv.buildImage()
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
                    echo "deploying $ENV"
                    gv.deployApp()
                }
            }
        }
    }   
}
