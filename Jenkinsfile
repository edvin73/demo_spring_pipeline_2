pipeline {
    agent any

     environment {
        APP_NAME = "springboot-demo"
        JAR_FILE = "target/${APP_NAME}.jar"
        DEV_SERVER = "frp014"
        USER=liv
        DEPLOY_PATH = "/users/liv/edvin/delivery/app"  
    }


    tools {
        maven 'Maven' 
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                // Add your checkout steps here
                checkout scm 
            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
                // Add your build steps here
                sh 'mvn clean install -DskipTests=true'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                // Add your test steps here
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                // sh 'scp target/demo-0.0.1-SNAPSHOT.jar liv@frp014:/users/liv/edvin/delivery/app/'
                    // ssh user@${DEV_SERVER} 'pkill -f ${APP_NAME}.jar || true'
                    // ssh user@${DEV_SERVER} 'nohup java -jar ${DEPLOY_PATH}/${APP_NAME}.jar --spring.profiles.active=prod > ${DEPLOY_PATH}/app.log 2>&1 &'
                sh """
                    ssh ${USER}@${DEV_SERVER}  
                    scp ${JAgR_FILE} ${USER}@${DEV_SERVER}:${DEPLOY_PATH}
                """

                echo 'Application deployed successfully.'


                // Add your deploy steps here
            }
        }
    }
}