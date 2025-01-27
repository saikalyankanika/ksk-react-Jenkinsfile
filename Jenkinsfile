@Library('shared-pipeline@master') _

pipeline {
    agent none
    stages {
        stage('INIT') {
            agent any // Allocate an agent for this stage
            steps {
                script {

                    sh "rm -rf ${env.WORKSPACE}/*"
                    // Clone the repository (shallow clone for efficiency)
                    sh 'git clone --no-checkout https://github.com/saikalyankanika/react-sample-ksk repo'
                    
                    dir('repo'){sh 'git checkout HEAD cicd-config.yaml'}

                    // Read the YAML file
                    def yamlFile = readFile(file: "${env.WORKSPACE}/repo/cicd-config.yaml")

                    // Manually parse the YAML file
                    yamlFile.split('\n').each { line ->
                        if (line.trim()) { // Skip empty lines
                            def (key, value) = line.split(':').collect { it.trim() }
                            env."${key}" = value
                            echo "${key} = ${value}"}}

                    def output_work = env.WORKSPACE
                    println "Current directory: ${output_work}"

                    echo sh(script: 'env|sort', returnStdout: true)

                    init("https://github.com/saikalyankanika/react-sample-ksk")

                }
            }
        }
    }
}

