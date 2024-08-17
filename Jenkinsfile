pipeline{
    agent any
    stages{
        stage("Cleanup"){
            steps{
                sh '''
                    docker ps -a --filter "ancestor=my_project" --format "{{.ID}}" | xargs docker stop
                    docker images -q my_project | xargs -r docker rmi -f
                '''
            }
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
    }
}
