pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
        jdk "jdk11"
    }

    stages {
        stage('compile') {
            steps {
                // Get some code from a GitHub repository
                git branch:'dev', 
                    url:'https://github.com/matthcol/movieapijava2021.git'

                // Run Maven on a Unix agent.
                sh "mvn clean compile"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }


        }
       
		
		
		stage('test') {
            steps {

                // Run Maven on a Unix agent.
                sh "mvn test"


            }
            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    
                }
            }

        }
        
		
		
		stage('package') {
            steps {
               

                // Run Maven on a Unix agent.
                sh "mvn -DskipTests package"


            }

            post {
                
                success {

                    archiveArtifacts 'target/*.jar'
                }
            }
        }
		
    }
}
