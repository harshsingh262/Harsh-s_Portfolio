pipeline{
    agent any
    stages{
        stage("Cleanup"){
            steps{
                sh 'docker images -q my_project | xargs -r rmi -f'
            }
        stage("Build_Image"){
            steps{
                sh 'docker build -t my_project .'
            }
        }
        stage("Production"){
            steps{
                sh 'docker run -it -d -p 82:80 my_project'
            }
        }
    }
}
