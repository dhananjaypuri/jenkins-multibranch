pipeline{
    agent any
    parameters {
        string(name: 'IMG_NAME', defaultValue: 'abc')
        choice(name: 'BUILD_ENVV', choices: ['master', 'dev'], description: "This is build env")
    }
    stages{
        stage("Build"){
            steps{
                echo "========Building========"

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
