node {

    stage('Clone Repository') {
         /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    try {
        stage('Build Image') {
            /* This builds actual image. synonymous to 
             * docker build on the command line */

            def app = docker.build("prateekstudytech/devops-tutorials")
        }

        stage('Test Image') {
        
            app.inside {
                sh 'echo "Test passed"'
            }
        }

        stage('Push Image') {
        
            docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-creds') {
                app.push("${env.BUILD_NUMBER}")
                app.push("latest")
            }
        }
    }

    finally {

        stage('Remove local image') {
            sh "docker rmi ${app.id}"
        }
    }
}

