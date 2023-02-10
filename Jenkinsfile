pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning..'
                // git clone git@github.com:Manssuresh/apache.git
            }
        }
        stage('Build') {
            steps {
                echo 'Building..'
               sh' zip -r index-$BUILD_NUMBER.zip index.html'
                sh 'aws s3 cp  index-$BUILD_NUMBER.zip s3://artifactory-bucket-kpkm/'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying....'
               sh 'rm -fr *'
               sh 'aws s3 cp s3://artifactory-bucket-kpkm/index-$BUILD_NUMBER.zip .'
               sh 'unzip index-$BUILD_NUMBER.zip'
               sh 'scp index.html root@172.31.1.135:/var/www/html/'

            }
        }
    }
        //     stage('Test') {
        //     steps {
        //         echo 'Testing..'
        //         curl -I http://43.207.31.99/
        //     }
        // }
}