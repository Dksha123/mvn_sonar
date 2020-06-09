pipeline {
     agent any
    stages {
        stage('Git Checkout') {
            steps {
                git 'https://github.com/Dksha123/mvn_sonar.git'
            }
        }
        stage(' Build analysis') {
            steps {
                withSonarQubeEnv('sonar') {
                    sh '/opt/maven/bin/mvn clean verify sonar:sonar -Dmaven.test.skip=true'
                }
            }
        }
        stage('Quality Gate') {
            steps {
                timeout(time: 2, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }

}
