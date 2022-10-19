pipeline {
    agent {
        label 'docker'
    }
    environment {
        PROJECT_NAME = "Project1111"
        OWNER_NAME   = "Dmitriy"
    }

    stages {
        stage('1-Build') {
            steps {
                echo 'Start of Stage Build'
                echo 'Building.........'
                sh "ls -la"
                echo 'End of stage Build'
            }
        }        
        stage('2-Test') {
            steps {
                echo 'Start of Stage Test'
                echo 'Testing.........'
                sh  """
                echo "Line1"
                echo "Line2"
                echo "Hello ${OWNER_NAME}"
                echo "Project name is ${PROJECT_NAME}"
                echo "Line3"
                """
                sh "python3 --version"
                echo 'End of stage Build'
            }
        }
        stage('3-Deploy') {
            steps {
                echo 'Start of Stage Deploy'
                echo 'Deploying.........'
                sh "pwd"
                echo 'End of stage Build'
            }
        }
        stage('4-Celebrate') {
            steps {
                echo "CONGRATULYACIYA!"
            }
        }
        stage("docker login") {
            steps {
                echo " =============== docker login ================"
                withCredentials([usernamePassword(credentialsId: 'dockerhub_mal', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh """
                    docker login -u $USERNAME -p $PASSWORD
                    """
                }
            }
        }
        stage("create docker image") {
            steps {
                echo " =========== start building image ============"
                dir ('docker') {
                    sh 'docker build -t dmitriy228/toolbox:latest . '
                }
            }
        }
        stage("docker push") {
            steps {
                echo " =============== start pushing image =============="
                sh '''
                docker push dmitriy228/toolbox:latest
                '''
            }
        }
   
   
    }
}
