pipeline {
    agent any
    stages {
        stage('build') {
            steps {
            	sh 'echo "building project"'
                sh 'mvn --version'
                sh 'mvn clean'
                sh 'mvn test'
                sh 'mvn install'
                sh 'mvn package'
            }
        }
		stage('Deploy') {
            steps {
            	sh 'echo "running program"'
                retry(3) {
                    sh 'java -cp java-maven-junit-helloworld-1.0-SNAPSHOT.jar com.example.javamavenjunithelloworld.HelloApp'
                }

                timeout(time: 3, unit: 'MINUTES') {
                    sh 'java -cp java-maven-junit-helloworld-1.0-SNAPSHOT.jar com.example.javamavenjunithelloworld.HelloApp'
                }
            }
        }
    }
	post {
        always {
            echo 'Building and running completed'
        }
        success {
            echo 'Project successfully build'
        }
        failure {
            echo 'Failed building project'
        }
    }
}
