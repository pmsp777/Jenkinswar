pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven"
    }

    stages {
        stage('gitcheckout') {
            steps {
             checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'git_token', url: 'https://github.com/pmsp777/Jenkinswar.git']])
            }
        }
        stage('build') {
            steps {
                bat'mvn clean install'
            }
        }
        stage('codequality') {
            steps {
            bat'mvn sonar:sonar'    
            }
        }
        stage('deploy') {
            steps {
             deploy adapters: [tomcat8(credentialsId: 'tomcat_cred', path: '', url: 'http://localhost:7000')], contextPath: 'pmsp777/Jenkinswar', war: '**/*.war'
            }
        }

             
                }
            }
        

