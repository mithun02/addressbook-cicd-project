pipeline {
    agent any
    stages {
        stage('GitHub Validation') {
            steps {
                git url: 'https://github.com/mithun02/addressbook-cicd-project.git'
            }
        }
        stage('Compiling the Code') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('Testing the Code') {
            steps {
                sh 'mvn test'
            }
        }
        stage('QA of the Code') {
            steps {
                sh 'mvn pmd:pmd'
            }
        }
        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Verify WAR File') {  // ✅ Debugging step
            steps {
                sh 'ls -lh /var/lib/jenkins/workspace/addressbookcicd/target/'
            }
        }
        stage('Deploy the Project on Tomcat') {
            steps {
                sh '''
                sudo cp /var/lib/jenkins/workspace/addressbookcicd/target/addressbook.war /home/mithun/apache-tomcat-9.0.93/webapps/
                sudo /home/mithun/apache-tomcat-9.0.93/bin/shutdown.sh
                sudo /home/mithun/apache-tomcat-9.0.93/bin/startup.sh
                '''
            }
        }
    }
}
