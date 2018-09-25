#!/usr/bin/env groovy

node {

    try {

        stage('checkout') {
            checkout scm
        }

        maintainer_name = "kaylene"
        container_name = "supervision-mysql-haproxy"
        registry_url = "https://index.docker.io/v1/"
        docker_creds_id = "docker-login"
        build_tag = "latest"

        def dockerImage
        stage('Docker build') {
            dockerImage = docker.build("${maintainer_name}/${container_name}")
        }

        stage('Docker publish') {
            docker.withRegistry("${registry_url}", "${docker_creds_id}") {
                dockerImage.push "${build_tag}"
            }
        }

    }
}
