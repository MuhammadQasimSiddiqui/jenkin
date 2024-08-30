pipeline {
    agent any // Specifies that the pipeline can run on any available agent/node

    parameters { // Defines parameters for the pipeline
        string(name: 'emailRecipient', defaultValue: 'muhammadqasimsiddiqui2000@gmail.com', description: 'Email address to receive notifications') // String parameter for recipient email address
        booleanParam(name: 'attachLog', defaultValue: true, description: 'Attach build log to email') // Boolean parameter for attaching build log to email
    }

    triggers { // Configuring triggers for the pipeline
        pollSCM('* * * * *') // Poll SCM every minute
    }

    stages { // Defines stages of the pipeline
        stage('Build') { // Defines the "Build" stage
            steps {
                echo 'Build the code using a build automation tool to compile and package your code. You need to specify at least one build automation tool e.g., Maven.' // Echoes a message describing the build stage
            }
        }
        stage('Unit and Integration Tests') { // Defines the "Unit and Integration Tests" stage
            steps {
                echo 'Run unit tests to ensure the code functions as expected and run integration tests to ensure the different components of the application work together as expected. You need to specify test automation tools for this stage.' // Echoes a message describing the unit and integration tests stage
            }
            post { // Defines post-build actions for the stage
                success { // Executes if the stage is successful
                    emailext( // Sends an email notification
                        subject: 'Unit & Integration Tests - Success!', // Email subject for successful stage
                        body: 'Unit and Integration Tests passed successfully in the latest version!', // Email body for successful stage
                        to: "${params.emailRecipient}", // Email recipient
                        attachLog: "${params.attachLog}", // Attach build log to email
                        mimeType: 'text/plain', // MIME type for the email content
                        debug: true // Enable debug mode to troubleshoot email sending
                    )
                }
                failure { // Executes if the stage fails
                    emailext( // Sends an email notification
                        subject: 'Unit & Integration Tests - Failed!', // Email subject for failed stage
                        body: 'Unit and Integration Tests failed! Check the logs for details.', // Email body for failed stage
                        to: "${params.emailRecipient}", // Email recipient
                        attachLog: "${params.attachLog}", // Attach build log to email
                        mimeType: 'text/plain', // MIME type for the email content
                        debug: true // Enable debug mode to troubleshoot email sending
                    )
                }
            }
        }
        stage('Code Analysis') { // Defines the "Code Analysis" stage
            steps {
                echo 'Integrate a code analysis tool to analyse the code and ensure it meets industry standards. Research and select a tool to analyse your code using Jenkins.' // Echoes a message describing the code analysis stage
            }
        }
        stage('Security Scan') { // Defines the "Security Scan" stage
            steps {
                echo 'Perform a security scan on the code using a tool to identify any vulnerabilities. Research and select a tool to scan your code.' // Echoes a message describing the security scan stage
            }
            post { // Defines post-build actions for the stage
                success { // Executes if the stage is successful
                    emailext( // Sends an email notification
                        subject: 'Security Scan - No Vulnerabilities Found!', // Email subject for successful stage
                        body: 'Security scan completed successfully - No vulnerabilities detected!', // Email body for successful stage
                        to: "${params.emailRecipient}", // Email recipient
                        attachLog: "${params.attachLog}", // Attach build log to email
                        mimeType: 'text/plain', // MIME type for the email content
                        debug: true // Enable debug mode to troubleshoot email sending
                    )
                }
                failure { // Executes if the stage fails
                    emailext( // Sends an email notification
                        subject: 'Security Scan - Vulnerabilities Found!', // Email subject for failed stage
                        body: 'Security scan detected vulnerabilities! Address them before deployment.', // Email body for failed stage
                        to: "${params.emailRecipient}", // Email recipient
                        attachLog: "${params.attachLog}", // Attach build log to email
                        mimeType: 'text/plain', // MIME type for the email content
                        debug: true // Enable debug mode to troubleshoot email sending
                    )
                }
            }
        }
        stage('Deploy to Staging') { // Defines the "Deploy to Staging" stage
            steps {
                echo 'Deploy the application to a staging server (e.g., AWS EC2 instance).' // Echoes a message describing the deploy to staging stage
            }
        }
        stage('Integration Tests on Staging') { // Defines the "Integration Tests on Staging" stage
            steps {
                echo 'Run integration tests on the staging environment to ensure the application functions as expected in a production-like environment.' // Echoes a message describing the integration tests on staging stage
            }
            post { // Defines post-build actions for the stage
                always { // Executes always, regardless of the stage result
                    emailext( // Sends an email notification
                        subject: 'Integration Tests on Staging - Complete!', // Email subject
                        body: 'Integration tests on Staging environment completed!', // Email body
                        to: "${params.emailRecipient}", // Email recipient
                        attachLog: "${params.attachLog}", // Attach build log to email
                        mimeType: 'text/plain', // MIME type for the email content
                        debug: true // Enable debug mode to troubleshoot email sending
                    )
                }
            }
        }
        stage('Deploy to Production') { // Defines the "Deploy to Production" stage
            steps {
                echo 'Deploy the application to a production server (e.g., AWS EC2 instance).' // Echoes a message describing the deploy to production stage
            }
        }
    }
}
