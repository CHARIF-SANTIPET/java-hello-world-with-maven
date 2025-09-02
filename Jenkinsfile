pipeline {
    agent any

    stages {
        stage('Maven Check') {
            steps {
                sh 'docker run -i --rm --name my-maven-project maven:3.9.9 mvn --version'
            }
        }
        stage('Build') {
            steps {
                sh 'docker run -i --rm --name my-maven-project --network jenkins-sonar-network -v "E:/Y4-1/AjKrit/sanor2/java-hello-world-with-maven:/usr/src/mymaven" -w /usr/src/mymaven maven:3.9.9 mvn clean install'
            }
        }

        stage('SonarQube') {
            steps {
                sh '''docker run -i --rm --name my-maven-project --network jenkins-sonar-network -v "E:/Y4-1/AjKrit/sanor2/java-hello-world-with-maven:/usr/src/mymaven" -w /usr/src/mymaven maven:3.9.9 mvn clean verify sonar:sonar -Dsonar.projectKey=SonarQube2 -Dsonar.projectName='SonarQube2' -Dsonar.host.url=http://sonarqube:9000 -Dsonar.token=sqp_b01ae511254d259260fed2c6fc612336cefe6b33'''
            }  
        }
    }
}
