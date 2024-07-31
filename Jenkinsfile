pipeline {
    agent any

    parameters {
        string(name: 'BRANCH_NAME', defaultValue: 'main', description: 'Branch to build')
        choice(name: 'BUILD_ENV', choices: ['development', 'training', 'production'], description: 'Environment to build')
        booleanParam(name: 'RUN_TESTS', defaultValue: true, description: 'Run tests after build')
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the branch specified in the parameter
                checkout([$class: 'GitSCM', branches: [[name: "*/${params.BRANCH_NAME}"]],
                userRemoteConfigs: [[url: 'https://github.com/AvisenaAlwi/belajar-jenkins.git']]])
            }
        }
        stage('Build') {
            steps {
                echo "Building branch ${params.BRANCH_NAME} for environment ${params.BUILD_ENV}"
                // Add your build steps here
                // sh './build.sh'
            }
        }
        stage('Test') {
            // Test hanya akan dijalankan jika param RUN_TEST dicentang atau true
            when {
                expression { return params.RUN_TESTS }
            }
            steps {
                echo 'Running tests...'
                // Add your test steps here
                // sh './run_tests.sh'
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying to ${params.BUILD_ENV} environment"
                // Add your deployment steps here
                // sh "./deploy.sh ${params.BUILD_ENV}"
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            // Add any cleanup steps here
            deleteDir()
        }
        success {
            echo 'success bro'
        }
        failure {
            echo 'Failure bro'
        }
    }
}
