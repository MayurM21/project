pipeline {
    agent {
        node {
            label "master"
            customWorkspace "/home/mayur/project"
        }
    }
    stages {
        stage ("Clone Repository") {
            steps {
                sh '''
                    rm -rf project/
                    git clone https://github.com/MayurM21/project.git -b dev
                    chmod -R 777 /home/mayur/project
                '''
            }
        }
        stage ("Compile Code") {
            steps {
                sh '''
                    rm -rf ~/.m2/repository
                    mvn -f project/pom.xml clean install
                '''
            }
        }
        stage ("Deploy") {
            agent {
                node {
                    label "slave-1"
                }
            }
            steps {
                sh '''
                    scp -i /home/mayur/mayur.pem -o StrictHostKeyChecking=no project/target/LoginWebApp.war \
                    mayur@172.31.11.224:/home/mayur/servers/apache-tomcat-9.0.98/webapps
                '''
            }
        }
        stage ("Start Server") {
            agent {
                node {
                    label "slave-1"
                }
            }

            options {
        skipDefaultCheckout()
    }
            
            steps {
                sh '''
                    chmod -R 777 /home/mayur/servers/apache-tomcat-9.0.98/webapps
                    nohup bash /home/mayur/servers/apache-tomcat-9.0.98/bin/shutdown.sh &
                    nohup bash /home/mayur/servers/apache-tomcat-9.0.98/bin/startup.sh &
                '''
            }
        }
    }
}
