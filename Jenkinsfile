#!groovy

MARKETS_COLLECTOR_ARTIFACT = 'mirrorgate-markets-collector.zip'

node ('global') {

    try {

        stage('Checkout') {
            checkout(scm)
        }

        stage('Build') {
            sh """
                #Commented until stop using git for dependencies
                #docker-compose -p \${BUILD_TAG} run -u \$(id -u) install
                npm install
            """
        }
        
        stage('Package Zip') {
            sh """
                docker-compose -p \${BUILD_TAG} run -u \$(id -u) package
            """
        }

        stage('Publish on Jenkins') {
      	    step([$class: "ArtifactArchiver", artifacts: "build/${MARKETS_COLLECTOR_ARTIFACT}", fingerprint: true])
        }

    } catch(Exception e) {
        throw e;
    }
}
