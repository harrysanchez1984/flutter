podTemplate(
    label: 'jenkins-pipeline',
    inheritFrom: 'default',
    containers: [
      containerTemplate(name: 'docker', image: 'docker:18.06', command: 'cat', ttyEnabled: true),
      containerTemplate(name: 'helm', image: 'lachlanevenson/k8s-helm:v3.2.4', command: 'cat', ttyEnabled: true),
      containerTemplate(name: 'chrome', image: 'zenika/alpine-chrome:83-with-node', command: 'cat', ttyEnabled: true),
      //containerTemplate(name: 'selenium', image: 'selenium/standalone-chrome:3.14', command: '', ttyEnabled: false, ports: [portMapping(containerPort: 4444)]),
      // beevelop/cordova:latest is a more up-to-date option but there is an issue with the openjdk path and the android build process
      containerTemplate(name: 'cordova', image: 'walterwhites/cordova:latest', command: 'cat', ttyEnabled: true),
    ]
) {

    node ('jenkins-pipeline') {
        stage('Get Angular Code') {
            echo 'Pulling Source Code..'
            checkout scm
        }

        stage('TEST') {
            steps {
                sh 'flutter test'
            }
        }
        stage('BUILD') {
            steps {
                sh '''
                  #!/bin/sh
                  flutter build apk --debug
                  '''
            }
        }
        stage('DISTRIBUTE') {
            steps {
                appCenter apiToken: 'f51cd29ba6b2d34a84cd99bc37348db77624c614',
                        ownerName: 'ranaranvijaysingh9-gmail.com',
                        appName: 'Flutter-Starter',
                        pathToApp: 'build/app/outputs/apk/debug/app-debug.apk',
                        distributionGroups: 'AlphaTester'
            }
        }


    }
}


