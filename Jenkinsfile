pipeline{
    agent any
    parameters {
        string(name: 'IMG_NAME', defaultValue: 'abc_flask')
        choice(name: 'BUILD_ENVV', choices: ['master', 'dev', 'stag'], description: "This is build env")
    }
    stages{
        stage("Build"){
            environment {
                NEW_IMG_NAME = "${params.IMG_NAME}_${params.BUILD_ENVV}"
                DOCKER_UNAME = "dhananjaypuri"
                DOCKER_CREDS = credentials('docker_secret_pass')
            }
            steps{
                echo "========Building Python Image========"
                sh '''
                docker build -t ${DOCKER_UNAME}/${NEW_IMG_NAME} .
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
