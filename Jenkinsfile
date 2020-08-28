pipeline {
    agent any

    environment {
        HOST_REMOTO = "<syspass-server>"
        PATH_REMOTO = "/opt/docker-compose/syspass"
    }

    stages {
        stage('Envio ao host do Docker') {
            steps {
                sshPublisher(
                    failOnError: true,
                    publishers: [
                        sshPublisherDesc(
                            configName: "${HOST_REMOTO}",
                            verbose: false,
                            transfers: [
                                sshTransfer(
                                    sourceFiles: '**/*',
                                    removePrefix: '',
                                    remoteDirectory: '',
                                )
                        ])
                ])
            }
        }

        stage('Start Compose') {
            steps {
                sshPublisher(
                    failOnError: true,
                    publishers: [
                        sshPublisherDesc(
                            configName: "${HOST_REMOTO}",
                            transfers: [
                                sshTransfer(
                                    execCommand: "sudo /usr/local/bin/docker-compose -f ${PATH_REMOTO}/docker-compose.yml up -d",
                                )
                        ])
                ])
            }
        }
    }

}
