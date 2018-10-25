@Library('github.com/rupalibehera/osio-pipeline@java_support') _

osio {

  config runtime: 'java'

  ci {
    

    def resources = processTemplate(params: [
          release_version: "1.0.${env.BUILD_NUMBER}"
    ])

    build resources: resources

  }

  cd {
    echo "Running CD build"

    def resources = processTemplate(params: [
          release_version: "1.0.${env.BUILD_NUMBER}"
    ])

    build resources: resources
    

  }
}
