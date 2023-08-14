pipeline{
    agent any
    parameters {
        string(name: 'IMG_NAME', defaultValue: 'abc_flask')
        choice(name: 'BUILD_ENVV', choices: ['master', 'dev', 'stag'], description: "This is build env")
    }
    stages{
        stage("Build"){
            steps{
                echo "========Building Python Image========"
                echo "${params.IMG_NAME}"

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
