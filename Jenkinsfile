podTemplate(
    containers: [
        containerTemplate(name: 'jnlp', image: 'jenkins/inbound-agent:jdk17', args: '${computer.jnlpmac} ${computer.name}'),
        containerTemplate(name: 'docker', image: 'docker:26.1.3', command: 'cat', ttyEnabled: true)
    ],
    volumes: [
        hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')
    ]
){
    node(POD_LABEL) {
       
        stage('Checkout Code') 
        {
            git branch: 'main', url: 'https://github.com/myoffice9899/simple-code-app'
            
        }
        stage('Docker build') {
            container("docker"){
                sh "docker build -t localhost:5001/$services:$tag -f ./$services/app.dockerfile ./$services"
            }
        }
        stage('Docker Push') {
            container("docker"){
                sh "docker push localhost:5001/$services:$tag"
            }
        }
    }
}