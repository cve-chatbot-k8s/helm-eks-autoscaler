pipeline {
    agent any
    environment {
        GH_TOKEN = credentials('github-credentials')
    }
    tools {
        nodejs 'node'
    }
    stages {
        stage('Lint commit messages') {
            when {
                not {
                    branch 'main'
                }
            }
            steps {
                sh 'npm install --save-dev @commitlint/config-conventional @commitlint/cli'
                sh 'npx commitlint --from=HEAD~1'
            }
        }
        stage('Helm Lint') {
            when {
                not {
                    branch 'main'
                }
            }
            steps {
                sh 'helm lint cluster-autoscaler'
            }
        }
        stage('Helm Template') {
            when {
                not {
                    branch 'main'
                }
            }
            steps {
                sh 'helm template cluster-autoscaler'
            }
        }
    }
}
