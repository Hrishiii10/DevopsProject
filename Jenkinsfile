pipeline {
    agent any

    environment {
        JIRA_SITE = 'https://mindcraftteam.atlassian.net/'
        JIRA_CREDENTIALS_ID = '91b08b9f-b17e-40e3-b539-4d6bae40d3d0'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Build logic (e.g., using Maven)
                    sh 'mvn clean package'

                    // Upload artifact to Nexus
                    nexusArtifactUploader artifacts: [[artifactId: 'your-artifact-id', file: 'target/your-artifact.jar', type: 'jar']],
                                          credentialsId: 'nexus-credentials-id',
                                          groupId: 'your-group-id',
                                          nexusUrl: 'http://nexus.yourdomain.com',
                                          nexusVersion: 'nexus3',
                                          protocol: 'http',
                                          repository: 'your-repository',
                                          version: '1.0.0'

                    // Update Jira
                    jiraComment(issueKey: 'JIRA-1234', comment: 'Code checked in and build successful.')
                    jiraTransitionIssue(issueKey: 'JIRA-1234', transition: 'In Progress')
                }
            }
        }

        stage('Deploy to Dev') {
            steps {
                script {
                    // Deployment logic for Dev environment
                    sh 'deploy to dev script'

                    // Update Jira
                    jiraComment(issueKey: 'JIRA-1234', comment: 'Deployment to Dev environment successful.')
                }
            }
        }

        stage('Deploy to SIT') {
            steps {
                script {
                    // Deployment logic for SIT environment
                    sh 'deploy to sit script'

                    // Update Jira
                    jiraComment(issueKey: 'JIRA-1234', comment: 'Deployment to SIT environment successful.')
                }
            }
        }

        stage('Deploy to UAT') {
            steps {
                script {
                    // Deployment logic for UAT environment
                    sh 'deploy to uat script'

                    // Update Jira
                    jiraComment(issueKey: 'JIRA-1234', comment: 'Deployment to UAT environment successful.')
                    jiraTransitionIssue(issueKey: 'JIRA-1234', transition: 'In UAT')
                }
            }
        }

        stage('Deploy to Prod') {
            steps {
                script {
                    // Deployment logic for Prod environment
                    sh 'deploy to prod script'

                    // Update Jira
                    jiraComment(issueKey: 'JIRA-1234', comment: 'Deployment to Production environment successful.')
                    jiraTransitionIssue(issueKey: 'JIRA-1234', transition: 'Done')
                }
            }
        }
    }
}
