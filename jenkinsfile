}

    stages {
        stage('Get Code') {
            steps {
                git branch: 'main', credentialsId: '52512e97-5ec3-4f86-8748-317d46d61c5a', url: 'https://github.com/nikhil23407/my-era.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar-server-25.1.0.102122') {
                    sh "mvn sonar:sonar"
                }
            }
        }

        stage('Code deploy') {
            steps {
                sshagent(['tomcat-server']) {
                    sh 'scp -o StrictHostKeyChecking=no target/02-maven-web-app.war admin@51.20.130.60:/home/admin/apache-tomcat-9.0.98/webapps'
                }
            }
        }
    }
}

