@Library('github.com/rupalibehera/osio-pipeline@java_support') _

osio {

  config runtime: 'java', version: '1.8.1'

  ci {


    def resources = processTemplate(params: [
          release_version: "1.0.${env.BUILD_NUMBER}"
    ])

    build resources: resources

  }

  cd {
    echo "Running CD build....."

    def resources = processTemplate(params: [
          release_version: "1.0.${env.BUILD_NUMBER}"
    ])

    build resources: resources
    deploy resources: resources, env: 'stage'
    deploy resources: resources, env: 'run', approval: 'manual'

  }
}
