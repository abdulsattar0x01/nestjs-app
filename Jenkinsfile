pipeline {

agent any

environment {
    CONTAINER_NAME = 'nestjs-app'
    IMAGE = 'nestjs-app-image'
    EMAIL = 'abdulsattar0x01@gmail.com'
    PORT = 3000
}

stages{ 

    stage("Clone Repository"){

        steps {
                git branch : 'main' , url: 'https://github.com/abdulsattar0x01/nestjs-app.git'
        }
    
    }

    stage("Build Docker Image"){

        steps {
                sh "docker build -t ${IMAGE} ." 
        }

    }

    stage("Stop and Remove Previous Container"){

        steps {
                sh "docker stop ${CONTAINER_NAME} || true"
                sh "docker rm ${CONTAINER_NAME} || true"
        } 

    }

    stage("Run Docker Container"){

        steps { 
                sh "docker run -d --name ${CONTAINER_NAME} -p ${PORT}:${PORT} ${IMAGE}"
        }

    }

    stage("Send Notification"){

        steps {
                script {
                        def message = "Docker container '${CONTAINER_NAME}' is up and running on port ${PORT}."
                        emailext(
                                to: "${EMAIL}",
                                subject: "Jenkins Notification: ${CONTAINER_NAME}",
                                body: message
                        )
                }
        }

    }
}


}