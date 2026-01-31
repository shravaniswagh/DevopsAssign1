pipeline {
    agent any

    stages {

        stage('Build') {
            when {
                branch 'main'
            }
            steps {
                echo "Building on main branch..."
                bat 'generate_dummy_jar.bat'
            }
        }

        stage('Run Tests') {
            when {
                anyOf {
                    branch 'main'
                    branch pattern: "feature/.*", comparator: "REGEXP"
                    branch pattern: "release/.*", comparator: "REGEXP"
                }
            }
            steps {
                echo "Running tests..."
                junit 'dummy_test.xml'
            }
        }

        stage('Security Scan') {
            when {
                branch pattern: "release/.*", comparator: "REGEXP"
            }
            steps {
                echo "Running security scan for release branch..."
                writeFile file: 'security-scan.txt', text: 'SCAN: OK'
                archiveArtifacts 'security-scan.txt'
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                echo "Deploying (dummy)..."
            }
        }
    }
}
