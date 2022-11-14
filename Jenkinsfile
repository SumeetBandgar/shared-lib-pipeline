@Library("shared-library") _

pipeline {
    agent any
    tools {
        maven 'MAVEN_HOME'
    }
    stages {
        stage("Checkout Repo") {
            steps {
                script{
                    properties([
                        parameters([
                            string(
                                defaultValue: 'https://github.com/SumeetBandgar/Java.git', 
                                name: 'REPO_URL', 
                                trim: true
                            ),
                            string(
                                defaultValue: 'hello-world-spring-boot', 
                                name: 'BRANCH_NAME', 
                                trim: true
                            )
                        ])
                    ])
                    buildApp.checkout(params.REPO_URL, params.BRANCH_NAME)
                }
            }
        }
        stage("Build Application") {
            steps {
                script{
                    buildApp.build()
                }
            }
            
            post {
                success {
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}