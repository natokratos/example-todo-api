node('php'){
    stage('clean') {
        deleteDir()
        sh 'ls -la'
    }
    stage('fetch') {
        git 'https://github.com/jeffersonsouza/example-todo-api.git'
    }
    stage('build'){
        sh 'composer install --prefer-dist --no-dev --ignore-platform-reqs'
        sh 'php artisan config:cache'
        //sh 'php artisan route:cache'
    }
    stage('docker-build') {
        echo 'Cria a imagem para ser enviada para o DockerHub'
        sh 'sudo docker build -t natokratos/todoapi:$BUILD_NUMBER . '
        //sh 'sudo docker build -t natokratos/todoapi:latest . '
    }
    stage('docker-ship') {
        echo 'Envia a imagem cria a para o DockerHub'
        sh 'sudo docker push natokratos/todoapi:$BUILD_NUMBER'
        //sh 'sudo docker push natokratos/todoapi:latest'
    }
    
    
}
