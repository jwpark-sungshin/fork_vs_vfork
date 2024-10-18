node {
    def app
    stage('Clone repository') {
        git 'https://github.com/lusnue/fork_vs_vfork.git'
    }
    stage('Build image') {
        app = docker.build("lusnue/test")
    }
    stage('Test image') {
        app.inside {
            sh 'make test'
        }
    }
    stage('Push image') {
        docker.withRegistry('https://hub.docker.com/repository/docker/lusnue/test', 'lusnue') {
           app.push("${env.BUILD_NUMBER}")
           app.push("latest")
        }
    }
}
