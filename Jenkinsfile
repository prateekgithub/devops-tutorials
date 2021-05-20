node {
    def app

    environment { 
        registry = "prateekstudytech/devops-tutorials"
        registryCredential = 'docker-hub-creds' 
        dockerImage = ''
    }

    stage('clone repository') {
         /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds actual image. synonymous to 
         * docker build on the command line */

       app = docker.build("prateekstudytech/devops-tutorials")
    }

    stage('Test image') {
        
        app.inside {
            sh 'echo "Test passed"'
        }
    }

    stage('push image') {
        
        docker.withRegistry('',registryCredential) {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}

