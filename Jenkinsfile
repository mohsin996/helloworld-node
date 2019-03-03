node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("docker.io/mohsin996/hellonode-first")
    }

    stage('Test image') {
        /* Some test script in between */

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        /* Finally, we'll push the image with build tag: */
        docker.withRegistry('', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
        }
    }
}
