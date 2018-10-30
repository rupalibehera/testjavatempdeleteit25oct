@Library('github.com/rupalibehera/osio-pipeline@java_support_v1') _
def utils = new io.openshift.Utils()

osio {

  config runtime: 'java'

  ci {
         integrationTestCmd =
         "mvn org.apache.maven.plugins:maven-failsafe-plugin:integration-test \
            org.apache.maven.plugins:maven-failsafe-plugin:verify \
            -Dnamespace.use.current=false -Dnamespace.use.existing=${utils.currentNamespace()} \
            -Dit.test=*IT -DfailIfNoTests=false -DenableImageStreamDetection=true \
            -P openshift-it"

    def resources = processTemplate(params: [
          release_version: "1.0.${env.BUILD_NUMBER}"
    ])

    build resources: resources, commands: integrationTestCmd

  }

  cd {
    echo "Running CD build........"

    def resources = processTemplate(params: [
          release_version: "1.0.${env.BUILD_NUMBER}"
    ])

    build resources: resources, commands: """
    mvn clean install
    """
    deploy resources: resources, env: 'stage'
    deploy resources: resources, env: 'run', approval: 'manual'

  }
}
