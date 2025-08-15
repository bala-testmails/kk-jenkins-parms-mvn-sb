pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3911"
        jdk 'JDK24'
    }

    stages {

        stage('Echo Version') {
            steps {
                sh 'echo Print Maven Version'
                sh 'mvn -version'
                sh "echo Sleep-Time - ${params.SLEEP_TIME}, Port - ${params.APP_PORT}, Branch - ${params.BRANCH_NAME}"
            }
        }
        
        stage('Build') {
            steps {
                // Get some code from Github repository
                // git branch: 'main', url: 'https://github.com/bala-testmails/jenkins-mvn-spring-boot-hello-world.git'
            
                // Run Maven Package CMD
                sh 'mvn clean package -DskipTests=true'
            }
        }
        
        stage('Test') {
            steps {
                // Script blocks are used to execute groovy code
                // script {
                //     for(int i = 0; i < 60; i++) {
                //         echo "${i + 1 }"
                //         sleep 1
                //     }
                // }
                
                sh 'mvn test'
            }
        }

        stage('Local Deployment') {
            steps {
                sh 'java -jar target/kk-jenkins-parms-mvn-sb-0.0.1-SNAPSHOT.jar > /dev/null &'
                // sh '''
                //     java -jar target/kk-jenkins-parms-mvn-sb-0.0.1-SNAPSHOT.jar > /dev/null &
    
                //     # Set timeout in seconds
                //     TIMEOUT=60
                //     START=$(date +%s)
                    
                //     # Wait until app responds or timeout occurs
                //     until curl -s http://localhost:8090 >/dev/null 2>&1; do
                //       echo "Waiting for app to start..."
                //       sleep 2
                    
                //       NOW=$(date +%s)
                //       ELAPSED=$((NOW - START))
                //       if [ $ELAPSED -ge $TIMEOUT ]; then
                //         echo "Timeout! App did not start within $TIMEOUT seconds."
                //         exit 1
                //       fi
                //     done
                // '''
            }
        }

        stage('Integration Test') {
            steps {
                sh "sleep ${params.SLEEP_TIME}"
                sh 'curl http://localhost:8090'
            }
        }
    }
}
