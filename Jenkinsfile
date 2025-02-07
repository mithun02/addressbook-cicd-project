pipeline{
    agent any
    stages{
        stage('github validation'){
          steps{
                 git url: 'https://github.com/akshu20791/addressbook-cicd-project'
          }
        }
        stage('compiling the code'){
          steps{
                 sh 'mvn compile'
          }
        }
        stage('testing the code'){
            steps{
                sh 'mvn test'
            }
        }
        stage('qa of the code'){
            steps{
                sh 'mvn pmd:pmd'
            }
        }
        stage('package'){
            steps{
                sh 'mvn package'
            }
        }
        stage('Deploy the project on Tomcat') {
            steps {
                sh '''
                sudo mv /var/lib/jenkins/workspace/addressbookcicd/target/addressbook.war /home/ubuntu/apache-tomcat-8.5.100/webapps/
                sudo /home/ubuntu/apache-tomcat-8.5.100/bin/shutdown.sh
                sudo /home/ubuntu/apache-tomcat-8.5.100/bin/startup.sh
                '''
            }
        }

    }
}
