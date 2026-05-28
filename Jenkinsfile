pipeline {
    agent any

    environment {
        // 这里可以定义通用环境变量，例如:
        // JAVA_HOME = '/usr/lib/jvm/java-11-openjdk'
    }

    options {
        skipStagesAfterUnstable()
        timeout(time: 60, unit: 'MINUTES')
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }
git commit -m "Add Jenkinsfile"             
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building project...'
                // 在这里添加你的构建命令，例如：
                // sh 'mvn clean package'
                // sh 'npm install && npm run build'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // 在这里添加你的测试命令，例如：
                // sh 'mvn test'
                // sh 'npm test'
            }
        }

        stage('Publish') {
            when {
                expression { return env.BRANCH_NAME ==~ /main|master|release.*/ }
            }
            steps {
                echo 'Publishing artifacts or deploying...'
                // 在这里添加发布/部署命令，例如：
                // sh 'docker build -t myapp:${BUILD_NUMBER} .'
                // sh 'docker push myapp:${BUILD_NUMBER}'
            }
        }
    }

    post {
        success {
            echo 'Pipeline 执行成功。'
        }
        unstable {
            echo 'Pipeline 不稳定，请检查测试或质量门。'
        }
        failure {
            echo 'Pipeline 执行失败。'
        }
        always {
            echo '完成 Jenkins 流水线。'
        }
    }
}
