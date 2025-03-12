pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Deakon07/Produccion_Segura_Nginx_Jenkins_Git.git'
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Detener y eliminar cualquier contenedor NGINX anterior
                    sh 'docker stop web-server || true'
                    sh 'docker rm web-server || true'
                    
                    // Ejecutar el contenedor NGINX con el nuevo index.html
                    sh '''
                    docker run -d --name web-server --network nginx-network \
                    -v "$WORKSPACE/index.html":/usr/share/nginx/html/index.html nginx
                    '''
                }
            }
        }
    }
}
