pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Deakon07/Produccion_Segura_Nginx_Jenkins_Git.git'
            }
        }
        stage('Pull Changes') {
            steps {
                script {
                    // Hacer git pull para obtener los cambios más recientes
                    sh 'git pull origin main'
                }
            }
        }
        stage('Stop and Remove Old Containers') {
            steps {
                script {
                    // Detener y eliminar el contenedor web-server anterior
                    sh 'docker stop web-server || true'
                    sh 'docker rm web-server || true'
                    
                    // Detener y eliminar el contenedor nginx-proxy anterior
                    sh 'docker stop nginx-proxy || true'
                    sh 'docker rm nginx-proxy || true'
                }
            }
        }
        stage('Deploy web-server') {
            steps {
                script {
                    // Ejecutar el contenedor NGINX con el nuevo index.html
                    sh '''
                    docker run -d --name web-server --network nginx-network \
                    -v "$WORKSPACE/index.html:/usr/share/nginx/html/index.html" nginx
                    '''
                }
            }
        }
        stage('Deploy nginx-proxy') {
            steps {
                script {
                    // Ejecutar el contenedor nginx-proxy con la configuración actualizada
                    sh '''
                    docker run -d --name nginx-proxy --network nginx-network \
                    -v "C:/Users/Usuario/Desktop/MASTER CIBERSEGURIDAD/trabajoLuis/nginx-config/nginx-proxy.conf":/etc/nginx/nginx.conf -p 80:80 nginx
                    '''
                }
            }
        }
    }
}
