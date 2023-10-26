Assignment 4:
Create a Declarative CI pipeline for java based project that contains various stages like
Code checkout
Run below stages in parallel
- Code stability.
- Code quality analysis.
- Code coverage analysis.
Generate a report for code quality & analysis.
Publish artifacts.
Send Slack and Email notifications.
The user should have the option to skip various scans in the build execution. And before publish there should be an approval stage to be set in place to approve or deny the publish and if approved the step should execute and the user should be notified post successful/failed
Repeat the same using Scripted Pipeline.


DECLARATIVE PIPELINE

pipeline {
    agent any
    tools {
        maven 'mvn'
    }
    parameters {
        booleanParam(name: 'skip_test', defaultValue: false, description: 'Set to true to skip the test stage')
    }

    stages {
        stage('Declarative CI Pipeline') {
            steps {
                echo 'This is Declarative Pipeline'
            }
        }
        stage('Code Checkout') {
            steps {
                echo 'Started Cloning'
                git 'https://github.com/samirkesare/DevOpsCodeDemo.git'
            }
        }
        stage('Parallel Phase') {
            parallel {
                stage('Code Stability') {
                    when { expression { params.skip_test != true } }
                    steps {
                        echo "Testing code stability"
                        sh 'mvn test'
                    }
                }
                stage('Code Quality Analysis') {
                    when { expression { params.skip_test != true } }
                    steps {
                        echo "Check code quality using PMD"
                        sh 'mvn pmd:pmd'
                    }
                }
                stage('Code Coverage Analysis') {
                    when { expression { params.skip_test != true } }
                    steps {
                        echo "Check code coverage analysis using Jacoco"
                        //sh 'mvn clean verify'
                        jacoco()
                    }
                }
            }
        }
        stage('Build Artifacts') {
            steps {
                echo 'Build Artifact'
                sh 'mvn package'
            }
        }
    
        stage('Approval') {
            steps {
                input message: 'Do you want to proceed with publishing?', ok: 'Approve'
            }
        }
        stage('Publish Artifacts') {
            steps {
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }
        }
    }
    
    post {
        success {
            script {
                emailext body: 'Job Succesfully Done', subject: 'Status of job', to: 'parsu176desai@gmail.com'
                slackSend channel: 'jenkin_task', message: 'Job run successfully'
            }
        }
        failure {
            script {
                emailext body: 'Job failed', subject: 'Status of job', to: 'parsu176desai@gmail.com'
                slackSend channel: 'jenkin_task', message: 'Job failed'
            }
        }
    }
}

![Screenshot from 2023-10-23 14-09-30](https://github.com/parsugit/ansible_practice/assets/132131379/1054324a-821c-4b00-b715-e1b60882e99f)

