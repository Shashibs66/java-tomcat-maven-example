#!/usr/local/bin/groovy
pipeline {
    agent { node { label 'master' } }

    environment {
        TEST_PREFIX = "test-IMAGE"
        
    }

    stages {
        
          stage("Build and start test image") {
            steps {
                sh "docker-composer build"
                sh "docker-compose up -d"
                waitUntilServicesReady
            }
        }

        stage("Run tests") {
            steps {
                sh "docker-compose exec -T php-fpm composer --no-ansi --no-interaction tests-ci"
                sh "docker-compose exec -T php-fpm composer --no-ansi --no-interaction behat-ci"
            }
        }

    }
