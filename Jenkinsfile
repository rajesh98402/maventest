pipeline {
    agent any
       stages {
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }
	stage('Test') {
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        
	}

	 stage('Deliver') {
            steps {

    // Make the output directory.
     bat "mkdir -p output"

    // Write an useful file, which is needed to be archived.
    writeFile file: "output/usefulfile.txt", text: "This file is useful, need to archive it."

    // Write an useless file, which is not needed to be archived.
    writeFile file: "output/uselessfile.md", text: "This file is useless, no need to archive it."


    // Archive the build output artifacts.
    archiveArtifacts artifacts: 'target/*.jar', 'output/*.txt', excludes: 'output/*.md'

            }
        }

    }
}
