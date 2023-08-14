pipeline{
    agent any

    parameters {
        string(name: 'IMG_NAME', defaultValue: 'abc_flask')
        choice(name: 'BUILD_ENVV', choices: ['master', 'dev', 'stag'], description: "This is build env")
    }

    environment {
                NEW_IMG_NAME = "${params.IMG_NAME}_${params.BUILD_ENVV}"
                DOCKER_UNAME = "dhananjaypuri"
                DOCKER_CREDS = credentials('docker_secret_pass')
    }

    stages{
        stage("Build"){

            steps{
                echo "========Building Python Image========"
                sh '''
                docker build -t ${DOCKER_UNAME}/${NEW_IMG_NAME} .
                '''

            }

        }

        stage("Publish Image"){
            steps {
                echo "Publishing image"
                sh '''
                if echo ${DOCKER_CREDS} | docker login -u ${DOCKER_UNAME} --password-stdin
                then
                    echo "Login succeded"
                else
                    echo "Login failed"
                '''
            }

        }

        stage("Deploy"){

            when {
                expression {
                    params.BUILD_ENVV == 'master'
                }
            }

            steps{

                echo "========Deploying========"
            }

        }

    }

}
