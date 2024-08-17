pipeline{
    agent any
    stages{
        stage("Build_Image"){
            steps{
                sh 'docker build -t my_website .'
            }
        }
        stage("Production"){
            steps{
                sh 'docker run -it -d -p 82:80 my_website'
            }
        }
    }
}