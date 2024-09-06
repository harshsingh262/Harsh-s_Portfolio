pipeline{
    agent any
    stages{
        // stage("Cleanup"){
        //     steps{
        //         sh '''
        //             docker ps -a --filter "ancestor=my_project" --format "{{.ID}}" | xargs docker stop
        //             docker images -q my_project | xargs -r docker rmi -f
        //         '''
        //     }
        }
        stage("Build_Image"){
            steps{
                sh 'docker build -t my_project .'
            }
        }
        stage("Production"){
            steps{
                sh 'docker run -it -d -p 8084:80 my_project'
            }
        }
         stage("Testimg"){

             
            steps{
                sh 'docker ps  --filter "ancestor=my_project" --format "{{.ID}}" | xargs docker logs'
            }
        }
        stage("Health Check"){
              steps {
        script {
                    echo 'Waiting for 10 seconds...'
                    sleep 10
                }
                
                // Check if the container is running
                script {
                    def containerName = 'my_project' // Replace with your container name
                    def status = sh(script: "docker ps --filter 'ancestor=my_project' --filter 'status=running' --format '{{.Names}}'", returnStdout: true).trim()
                    
                    if (status) {
                        echo "Container '${containerName}' is running."
                    } else {
                        error "Container '${containerName}' is not running."
                    }
                }
        }
        }
    }
}
